# Global Movie & Webseries Recommendation System

This repository provides a **large-scale content recommendation system** for movies and web series. It includes:

1. **Dataset Generation**: A script to create a synthetic **100,000-row CSV** of movies and web series with varied columns (title, year, genre, keywords, etc.).  
2. **Recommendation Engine**: A system that takes the generated CSV, prompts the user to choose Movie/Webseries, then recommends similar items using **cosine similarity** and **TF-IDF** on combined text features.

## Table of Contents
- [Features](#features)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Usage](#usage)
  - [1. Generating the Dataset](#1-generating-the-dataset)
  - [2. Running the Recommendation Engine](#2-running-the-recommendation-engine)
- [How It Works](#how-it-works)
- [Dependencies](#dependencies)
- [Customization](#customization)
- [License](#license)
- [Contact](#contact)

---

## Features

- **Large Synthetic Dataset**: Generates 100,000 rows of data combining real-ish movie/web series titles, varied genres, cast members, directors, and more.
- **Improved Variety**: Reduces repetition by using extensive lists of titles, cast, and directors.
- **TF-IDF Based Similarity**: Combines metadata (genres, keywords, cast, director, tagline) into a single text string, then uses TF-IDF + cosine similarity for recommendations.
- **1 x N Computation**: Efficiently computes the similarity of the chosen item against all items, rather than building a large NxN matrix.

---

## Project Structure

```
├── generate_data.py               # Script to generate the 100K-row dataset
├── recommendation_engine.py       # Script to run the interactive recommendation system
├── final_100k_movies_webseries.csv    # Generated CSV file (after you run generate_data.py)
├── MovieRecommendationSystem.ipynb    # (Optional) Jupyter Notebook version (if any)
├── README.md                      # Project documentation
└── requirements.txt               # Optional: pinned dependencies
```

---

## Getting Started

1. **Clone** this repository or **download** the source code.
2. Ensure you have a **Python 3.x** environment set up (e.g., via `venv` or `conda`).

---

## Usage

### 1. Generating the Dataset

Run:
```bash
python generate_data.py
```

This creates a file called **`final_100k_movies_webseries.csv`** in the same directory, containing 100,000 rows of synthetic data. Each row represents either a **Movie** or a **Webseries**, with columns:

- `title`  
- `Type` (`Movie` or `Webseries`)  
- `Year`  
- `genres`  
- `keywords`  
- `tagline`  
- `cast`  
- `director`  
- `Country`  
- `index`  

> **Note**: This script can take some time due to the sheer number of rows, but it should be manageable for most modern systems.

### 2. Running the Recommendation Engine

After generating the dataset, run:
```bash
python recommendation_engine.py
```

The system will:

1. Prompt you to choose **Movie** or **Webseries**.  
2. Display a handful of titles from that category.  
3. Ask you to **enter a favorite title** (either from the listed ones or any known title in that category).  
4. Find the **closest match** (in case of minor spelling differences).  
5. Compute **cosine similarity** (1 x N) between your chosen item and all others.  
6. Print the **top recommendations** (up to 30).

---

## How It Works

1. **Dataset Generation**:
   - Each row is randomly assigned to be either a **Movie** or **Webseries**.
   - Titles, genres, cast, and other metadata are pulled from extended lists to ensure variety.
   - Year and taglines are generated realistically based on type.

2. **Recommendation**:
   - Filters dataset by user-selected content type.
   - Combines `genres`, `keywords`, `tagline`, `cast`, `director` into a single text string.
   - Builds TF-IDF vector for each row, finds the most similar entries using **cosine similarity**.
   - Only computes **1 x N** similarity (for scalability).

---

## Dependencies

- **Python 3.x**
- [NumPy](https://pypi.org/project/numpy/)
- [Pandas](https://pypi.org/project/pandas/)
- [scikit-learn](https://pypi.org/project/scikit-learn/)

Install them with:
```bash
pip install -r requirements.txt
```
Or individually:
```bash
pip install numpy pandas scikit-learn
```

---

## Customization

- **Expand the lists** in `generate_data.py` to further reduce repetition.
- Adjust the number of rows (default is 100k).
- Add new columns like `rating`, `runtime`, or `language` if desired.
- Replace synthetic data with real datasets (e.g., TMDB, IMDb) for more realism.

---

## License

This project is open-source under the MIT License.

---

## Contact

For any questions or suggestions, please open an **Issue** or reach out via:

- **Author**: *Your Name*  
- **Email**: *you@example.com*

---
*Thank you for using the Global Movie & Webseries Recommendation System!*