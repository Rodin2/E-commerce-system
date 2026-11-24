# NileByte Systems — HR Policy RAG Pipeline

نظام **Retrieval-Augmented Generation (RAG)** مبني داخل [`NileByte_Systems_Updated.ipynb`](https://colab.research.google.com/drive/1OqtqQlnQnodHYP-H7kgDNa663cDxpBdo#scrollTo=step-5-run-tests) للإجابة عن سياسات الموارد البشرية والعمل في **NileByte Systems** بالاعتماد على قاعدة معرفة داخلية (7 سياسات)، مع الاستشهاد بالمصادر (`[Doc X]`) ومنع الهلوسة عند الأسئلة غير الموجودة في السياسات.

## آلية العمل

1. **قاعدة المعرفة (`knowledge_base`):** 7 وثائق نصية تغطي العمل عن بُعد، الإجازة السنوية، مواعيد العمل، صرف الرواتب، بدل الإنترنت واللابتوب، السفر للعمل، والإجازة المرضية.
2. **الاسترجاع الدلالي (`Semantic Retriever`):** تضمين النصوص عبر `gemini-embedding-001` بأبعاد `(7, 3072)`، وتطبيع المتجهات (`L2-normalized`)، ثم ترتيب النتائج بالضرب النقطي (`top_k=3`, `min_score=0.35`).
3. **التوليد مع Citations وFallback:** إجبار النموذج على الاعتماد على الوثائق المسترجعة فقط مع كتابة `[Doc X]` والرد بعبارة ثابتة عند غياب المعلومة، مع تجربة النماذج بالترتيب: `gemini-3.5-flash-lite` ثم `gemini-3.5-flash` ثم `gemini-3.6-flash`.

## التشغيل

- افتحي النوتبوك في [Google Colab](https://colab.research.google.com/drive/1OqtqQlnQnodHYP-H7kgDNa663cDxpBdo#scrollTo=step-5-run-tests) وأضيفي `GEMINI_API_KEY` في Colab Secrets.
- شغّلي الخلايا من **Step 1** إلى **Step 5** (تتطلب `google-genai` و`numpy`).
