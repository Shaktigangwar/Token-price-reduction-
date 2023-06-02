

python

import spacy

def reduce_token_count(prompt_text, max_token_count):

    # Load the spaCy language model

    nlp = spacy.load('en_core_web_sm')

    

    # Tokenize the prompt text

    doc = nlp(prompt_text)

    

    # Calculate the current token count

    current_token_count = len(doc)

    

    # Check if the prompt text is already within the token limit

    if current_token_count <= max_token_count:

        return prompt_text

    

    # Initialize the reduced prompt text

    reduced_prompt_text = ''

    

    # Iterate through each token in the prompt text

    for token in doc:

        # Check if adding the token will exceed the token limit

        if len(reduced_prompt_text) + len(token.text) + 1 <= max_token_count:

            # Add the token to the reduced prompt text

            reduced_prompt_text += token.text_with_ws

        else:

            break  # Stop adding tokens if the limit is reached

    

    return reduced_prompt_text.strip()

# Example usage

prompt = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed convallis ultricies lacus."

max_token_count = 10

reduced_prompt = reduce_token_count(prompt, max_token_count)

print(reduced_prompt)



