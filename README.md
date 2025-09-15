Study Companion: Intelligent Learning Assistant
Inspiration
The inspiration for the Study Companion project came from my own struggles as a student when preparing for exams. I realized that even though we often have a syllabus, lecture notes, and textbooks, it’s difficult to connect them efficiently. What I wanted was a system that not only retrieved relevant information but also helped me practice through quizzes, guided hints, and suggestions on what to study next. The idea grew into a personalized AI study partner, one that blends search, reasoning, and tutoring.
What I Learned
While building this, I learned about several key areas:
	Vectorization techniques for text, and how turning syllabus items into embeddings makes them searchable by meaning rather than by keyword.
	Full-text search indexing (like with BM25) and how it complements embeddings by retrieving precise textbook references.
	LLM orchestration: combining different retrieval methods with prompt templates to generate useful outputs.
	Math problem handling: instead of forcing an LLM to solve math (which might be unreliable), integrating an external calculator/solver API ensures correctness for equations such as
∫▒  x^2  dx=x^3/3+C
	The importance of user experience design—students need trust, not just flashy results.
How I Built It
I approached building the Study Companion in modular steps:
	Syllabus ingestion & vectorization
	Each section of the syllabus is split, embedded into vectors using a transformer model, and stored in a vector database.
	Textbook ingestion & indexing
	The full body of the course textbook is run through a search engine indexer (e.g., ElasticSearch or Whoosh) allowing keyword-driven retrieval for precise context.
	Hybrid Retrieval
	Student queries first go through a hybrid system: semantic matches from syllabus vectors plus literal matches from textbook full-text search. This ensures both broad relevance and precise results.
	LLM Response Layer
	Retrieved information feeds into an LLM that performs three roles:
	Generate practice quizzes related to the material.
	Provide hints and solutions scaffolding for conceptual tough spots.
	Suggest what to study next based on syllabus progression.
	Math Support via API
	If a student asks something like:
"Solve x^2-5x+6=0"
The system delegates this to an external API that returnsx=2 "or" x=3and then the LLM wraps it into a teaching explanation.
Challenges Faced
Building this system wasn’t smooth—some of the challenges were:
	Context fusion: Combining syllabus vectors with textbook passages caused occasional duplication or irrelevant overlap. I had to experiment with re-ranking strategies.
	API management: Ensuring that math calculations were always correct without over-querying the external solver required careful integration.
	Prompt reliability: Sometimes the LLM would summarize instead of teaching. I had to fine-tune prompts with more examples of interactive teaching styles.
	Efficiency trade-offs: Vector searches were fast, but indexing large PDFs for full-text search was resource heavy. Optimizing retrieval pipelines was essential.
	User trust: A major challenge was making output that students believed in. This meant citing references, showing which syllabus section a quiz came from, and highlighting the textbook page.
