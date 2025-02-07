Steps Followed
1. Setting Up the AWS Environment
•	Created an S3 bucket to store the PDF documents.
•	Configured an AWS IAM role with appropriate permissions for Bedrock and S3.
•	Initialized AWS credentials using boto3.
2. Installing Required Libraries
•	Installed langchain, langchain_community, langchain_aws, faiss-cpu, and boto3.
•	Activated a Conda virtual environment and ensured dependencies were installed.
3. Loading and Processing the PDF Document
•	Used pypdf to extract text from a local PDF file.
•	Processed the extracted text into manageable chunks for embedding.
4. Generating Vector Embeddings with AWS Bedrock
•	Used BedrockEmbeddings from langchain_aws to generate vector embeddings.
•	Stored the vectors in FAISS index for efficient retrieval.
5. Querying the Document with Llama 3
•	Loaded the FAISS index and retrieved relevant document chunks.
•	Passed the retrieved text as context to the Llama 3 8B Instruct v1 model.
•	Displayed the response in the VS Code terminal.


Issues Encountered
1. ModuleNotFoundError for langchain_community
•	The import statement for BedrockEmbeddings was outdated.
•	Fixed by replacing from langchain.llms import Bedrock with from langchain_community.llms import Bedrock.
2. FAISS Index Not Found Error
•	The script attempted to load a FAISS index that did not exist.
•	Fixed by ensuring that the FAISS index was created before loading.
3. allow_dangerous_deserialization Warning in FAISS
•	FAISS requires explicit permission to deserialize pickle files.
•	Fixed by setting allow_dangerous_deserialization=True in FAISS.load_local().
4. AccessDeniedException When Using AWS Bedrock
•	The IAM role did not have permission to invoke the Llama 3 model.
•	Fixed by adding bedrock:InvokeModel permissions in the IAM policy.
5. No PDF Found in Local Directory
•	The script could not find the PDF file to process.
•	Fixed by placing the PDF file in the correct directory before running the script.
