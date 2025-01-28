# HomeMatch Documentation

## Overview

HomeMatch is a real estate listing generator and search system that uses OpenAI's language models and embeddings to create, store, and search through realistic property listings in Singapore. The system includes features for generating listings, semantic search, and personalized listing descriptions based on buyer preferences.

## Prerequisites

* Python 3.x
* Valid OpenAI API credentials
* Google Colab environment (for notebook execution)

## Dependencies

The following Python packages are required:

* `langchain_community`
* `chromadb`
* `tiktoken`
* `openai`
* `json`

## Installation

Run the following commands to install the required packages:

```bash
pip install langchain_community
pip install chromadb
pip install tiktoken
```

## Setting Up API Credentials

Before running the code, set up your OpenAI API credentials:

```python
import os
os.environ["OPENAI_API_KEY"] = "your-api-key"
os.environ["OPENAI_API_BASE"] = "your-api-base-url"
```

## Core Features

### 1. Listing Generation

The `generate_real_estate_listings()` function creates realistic property listings using OpenAI's language model.

```python
def generate_real_estate_listings(num_listings=10):
    """
    Generates realistic real estate listings in Singapore.
    
    Args:
        num_listings (int): Number of listings to generate (default: 10)
    
    Returns:
        list: Generated property listings in JSON format
    """
```

### 2. Vector Database Storage

The system uses ChromaDB to store and index listings for efficient semantic search:

* Creates embeddings for each listing using OpenAI's embedding model
* Stores listings with metadata for easy retrieval
* Handles JSON parsing and metadata formatting

### 3. Semantic Search

The `semantic_search()` function enables natural language search across listings:

```python
def semantic_search(query_text, n_results=2):
    """
    Performs semantic search on real estate listings.
    
    Args:
        query_text (str): Search query in natural language
        n_results (int): Number of results to return (default: 2)
    
    Returns:
        dict: Search results with relevant listings
    """
```

### 4. Personalized Listing Descriptions

The `augment_listing_description()` function customizes listing descriptions based on buyer preferences:

```python
def augment_listing_description(listing, buyer_preferences):
    """
    Augments listing descriptions based on buyer preferences.
    
    Args:
        listing (dict): Original listing data
        buyer_preferences (str): Description of buyer preferences
    
    Returns:
        str: Personalized listing description
    """
```

## Usage Examples

### 1. Generating Listings

```python
# Generate 5 listings
listings = generate_real_estate_listings(5)  
for listing in listings:
    print(listing)
```

### 2. Performing a Search

```python
# Define search query
query = "luxury condo near Orchard Road with 3 bedrooms and a swimming pool"
results = semantic_search(query, n_results=3)

# Display results
for i, doc in enumerate(results['documents'][0]):
    print(f"\nResult {i + 1}:")
    listing = json.loads(doc)
    print(json.dumps(listing, indent=2))
```

### 3. Personalizing Listings

```python
buyer_preferences = "young professional, enjoys nightlife, and is looking for a modern condo with easy access to public transport"
augmented_listing = augment_listing_description(listing, buyer_preferences)
print(augmented_listing)
```

## Error Handling

The system includes error handling for:

* JSON parsing errors
* API connection issues
* ChromaDB collection management
* Empty search results

## Best Practices

1. Adjust the OpenAI temperature parameter (0.7 by default) to control creativity in generated listings
2. Use specific search queries for better results
3. Provide detailed buyer preferences for more relevant personalization
4. Handle JSON parsing errors when working with generated listings

## Limitations

* Requires active internet connection for API calls
* Dependent on OpenAI API availability
* Generated listings are synthetic and should be verified for accuracy
* Search results quality depends on the embedding model's performance

## Troubleshooting

If you encounter issues:

1. Verify API credentials are correctly set
2. Check internet connectivity
3. Ensure all dependencies are installed
4. Verify JSON formatting in generated listings
5. Check ChromaDB collection existence and access

## Data Management

* Listings are stored in ChromaDB with embeddings
* Each listing includes metadata for filtering
* Search results include relevance scores
* Collection can be retrieved or created as needed

---

For more information or support, please refer to the individual package documentation:

* [LangChain Documentation](https://python.langchain.com/docs/get_started/introduction.html)
* [ChromaDB Documentation](https://docs.trychroma.com/)
* [OpenAI API Documentation](https://platform.openai.com/docs/introduction)
