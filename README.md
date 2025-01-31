{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "23e88196-2275-460e-bd0a-13a02cd74e25",
   "metadata": {},
   "source": [
    "LEVEL 1 - TASK 1: TOP CUISINES"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "46ab07c0-7632-4d1c-9d3e-4efa18b939c1",
   "metadata": {},
   "source": [
    "-- 1:1 Determine the top three most common cuisines in the dataset"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a4c028a8-c390-4825-9ed9-b6b21eac7fba",
   "metadata": {},
   "source": [
    "-- 1:2 Calculate the percentage of restaurants that serve each of the top cuisines"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b4b86abd-458b-4dde-bfc6-97a3dc38b14c",
   "metadata": {},
   "source": [
    "1:1 DETERMINE THE TOP THREE MOST COMMON CUISINES IN THE DATASET."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "4dc7e12b-c5d0-4294-8485-697522e3e6ba",
   "metadata": {},
   "outputs": [],
   "source": [
    "#import libraries\n",
    "import pandas as pd\n",
    "import numpy as np\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "ccdd56f2-f754-401d-8c8b-86d2f6786c23",
   "metadata": {},
   "outputs": [],
   "source": [
    "#import data\n",
    "dataset = pd.read_csv(\"Dataset.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "ca93a82d-7799-456a-b88f-5fb77e66472f",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Restaurant ID</th>\n",
       "      <th>Restaurant Name</th>\n",
       "      <th>Country Code</th>\n",
       "      <th>City</th>\n",
       "      <th>Address</th>\n",
       "      <th>Locality</th>\n",
       "      <th>Locality Verbose</th>\n",
       "      <th>Longitude</th>\n",
       "      <th>Latitude</th>\n",
       "      <th>Cuisines</th>\n",
       "      <th>...</th>\n",
       "      <th>Currency</th>\n",
       "      <th>Has Table booking</th>\n",
       "      <th>Has Online delivery</th>\n",
       "      <th>Is delivering now</th>\n",
       "      <th>Switch to order menu</th>\n",
       "      <th>Price range</th>\n",
       "      <th>Aggregate rating</th>\n",
       "      <th>Rating color</th>\n",
       "      <th>Rating text</th>\n",
       "      <th>Votes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>6317637</td>\n",
       "      <td>Le Petit Souffle</td>\n",
       "      <td>162</td>\n",
       "      <td>Makati City</td>\n",
       "      <td>Third Floor, Century City Mall, Kalayaan Avenu...</td>\n",
       "      <td>Century City Mall, Poblacion, Makati City</td>\n",
       "      <td>Century City Mall, Poblacion, Makati City, Mak...</td>\n",
       "      <td>121.027535</td>\n",
       "      <td>14.565443</td>\n",
       "      <td>French, Japanese, Desserts</td>\n",
       "      <td>...</td>\n",
       "      <td>Botswana Pula(P)</td>\n",
       "      <td>Yes</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>3</td>\n",
       "      <td>4.8</td>\n",
       "      <td>Dark Green</td>\n",
       "      <td>Excellent</td>\n",
       "      <td>314</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>6304287</td>\n",
       "      <td>Izakaya Kikufuji</td>\n",
       "      <td>162</td>\n",
       "      <td>Makati City</td>\n",
       "      <td>Little Tokyo, 2277 Chino Roces Avenue, Legaspi...</td>\n",
       "      <td>Little Tokyo, Legaspi Village, Makati City</td>\n",
       "      <td>Little Tokyo, Legaspi Village, Makati City, Ma...</td>\n",
       "      <td>121.014101</td>\n",
       "      <td>14.553708</td>\n",
       "      <td>Japanese</td>\n",
       "      <td>...</td>\n",
       "      <td>Botswana Pula(P)</td>\n",
       "      <td>Yes</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>3</td>\n",
       "      <td>4.5</td>\n",
       "      <td>Dark Green</td>\n",
       "      <td>Excellent</td>\n",
       "      <td>591</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>6300002</td>\n",
       "      <td>Heat - Edsa Shangri-La</td>\n",
       "      <td>162</td>\n",
       "      <td>Mandaluyong City</td>\n",
       "      <td>Edsa Shangri-La, 1 Garden Way, Ortigas, Mandal...</td>\n",
       "      <td>Edsa Shangri-La, Ortigas, Mandaluyong City</td>\n",
       "      <td>Edsa Shangri-La, Ortigas, Mandaluyong City, Ma...</td>\n",
       "      <td>121.056831</td>\n",
       "      <td>14.581404</td>\n",
       "      <td>Seafood, Asian, Filipino, Indian</td>\n",
       "      <td>...</td>\n",
       "      <td>Botswana Pula(P)</td>\n",
       "      <td>Yes</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>4</td>\n",
       "      <td>4.4</td>\n",
       "      <td>Green</td>\n",
       "      <td>Very Good</td>\n",
       "      <td>270</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>6318506</td>\n",
       "      <td>Ooma</td>\n",
       "      <td>162</td>\n",
       "      <td>Mandaluyong City</td>\n",
       "      <td>Third Floor, Mega Fashion Hall, SM Megamall, O...</td>\n",
       "      <td>SM Megamall, Ortigas, Mandaluyong City</td>\n",
       "      <td>SM Megamall, Ortigas, Mandaluyong City, Mandal...</td>\n",
       "      <td>121.056475</td>\n",
       "      <td>14.585318</td>\n",
       "      <td>Japanese, Sushi</td>\n",
       "      <td>...</td>\n",
       "      <td>Botswana Pula(P)</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>4</td>\n",
       "      <td>4.9</td>\n",
       "      <td>Dark Green</td>\n",
       "      <td>Excellent</td>\n",
       "      <td>365</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>6314302</td>\n",
       "      <td>Sambo Kojin</td>\n",
       "      <td>162</td>\n",
       "      <td>Mandaluyong City</td>\n",
       "      <td>Third Floor, Mega Atrium, SM Megamall, Ortigas...</td>\n",
       "      <td>SM Megamall, Ortigas, Mandaluyong City</td>\n",
       "      <td>SM Megamall, Ortigas, Mandaluyong City, Mandal...</td>\n",
       "      <td>121.057508</td>\n",
       "      <td>14.584450</td>\n",
       "      <td>Japanese, Korean</td>\n",
       "      <td>...</td>\n",
       "      <td>Botswana Pula(P)</td>\n",
       "      <td>Yes</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>No</td>\n",
       "      <td>4</td>\n",
       "      <td>4.8</td>\n",
       "      <td>Dark Green</td>\n",
       "      <td>Excellent</td>\n",
       "      <td>229</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows × 21 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   Restaurant ID         Restaurant Name  Country Code              City  \\\n",
       "0        6317637        Le Petit Souffle           162       Makati City   \n",
       "1        6304287        Izakaya Kikufuji           162       Makati City   \n",
       "2        6300002  Heat - Edsa Shangri-La           162  Mandaluyong City   \n",
       "3        6318506                    Ooma           162  Mandaluyong City   \n",
       "4        6314302             Sambo Kojin           162  Mandaluyong City   \n",
       "\n",
       "                                             Address  \\\n",
       "0  Third Floor, Century City Mall, Kalayaan Avenu...   \n",
       "1  Little Tokyo, 2277 Chino Roces Avenue, Legaspi...   \n",
       "2  Edsa Shangri-La, 1 Garden Way, Ortigas, Mandal...   \n",
       "3  Third Floor, Mega Fashion Hall, SM Megamall, O...   \n",
       "4  Third Floor, Mega Atrium, SM Megamall, Ortigas...   \n",
       "\n",
       "                                     Locality  \\\n",
       "0   Century City Mall, Poblacion, Makati City   \n",
       "1  Little Tokyo, Legaspi Village, Makati City   \n",
       "2  Edsa Shangri-La, Ortigas, Mandaluyong City   \n",
       "3      SM Megamall, Ortigas, Mandaluyong City   \n",
       "4      SM Megamall, Ortigas, Mandaluyong City   \n",
       "\n",
       "                                    Locality Verbose   Longitude   Latitude  \\\n",
       "0  Century City Mall, Poblacion, Makati City, Mak...  121.027535  14.565443   \n",
       "1  Little Tokyo, Legaspi Village, Makati City, Ma...  121.014101  14.553708   \n",
       "2  Edsa Shangri-La, Ortigas, Mandaluyong City, Ma...  121.056831  14.581404   \n",
       "3  SM Megamall, Ortigas, Mandaluyong City, Mandal...  121.056475  14.585318   \n",
       "4  SM Megamall, Ortigas, Mandaluyong City, Mandal...  121.057508  14.584450   \n",
       "\n",
       "                           Cuisines  ...          Currency Has Table booking  \\\n",
       "0        French, Japanese, Desserts  ...  Botswana Pula(P)               Yes   \n",
       "1                          Japanese  ...  Botswana Pula(P)               Yes   \n",
       "2  Seafood, Asian, Filipino, Indian  ...  Botswana Pula(P)               Yes   \n",
       "3                   Japanese, Sushi  ...  Botswana Pula(P)                No   \n",
       "4                  Japanese, Korean  ...  Botswana Pula(P)               Yes   \n",
       "\n",
       "  Has Online delivery Is delivering now Switch to order menu Price range  \\\n",
       "0                  No                No                   No           3   \n",
       "1                  No                No                   No           3   \n",
       "2                  No                No                   No           4   \n",
       "3                  No                No                   No           4   \n",
       "4                  No                No                   No           4   \n",
       "\n",
       "   Aggregate rating  Rating color Rating text Votes  \n",
       "0               4.8    Dark Green   Excellent   314  \n",
       "1               4.5    Dark Green   Excellent   591  \n",
       "2               4.4         Green   Very Good   270  \n",
       "3               4.9    Dark Green   Excellent   365  \n",
       "4               4.8    Dark Green   Excellent   229  \n",
       "\n",
       "[5 rows x 21 columns]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#display the first few rows to understand its structure \n",
    "dataset.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "49a72952-9852-45ec-be59-0f448e6a5752",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(9551, 21)"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#check database shape (rows and column)\n",
    "dataset.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "a755739d-8aa2-4e1d-9ec3-5d4ff461896a",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 9551 entries, 0 to 9550\n",
      "Data columns (total 21 columns):\n",
      " #   Column                Non-Null Count  Dtype  \n",
      "---  ------                --------------  -----  \n",
      " 0   Restaurant ID         9551 non-null   int64  \n",
      " 1   Restaurant Name       9551 non-null   object \n",
      " 2   Country Code          9551 non-null   int64  \n",
      " 3   City                  9551 non-null   object \n",
      " 4   Address               9551 non-null   object \n",
      " 5   Locality              9551 non-null   object \n",
      " 6   Locality Verbose      9551 non-null   object \n",
      " 7   Longitude             9551 non-null   float64\n",
      " 8   Latitude              9551 non-null   float64\n",
      " 9   Cuisines              9542 non-null   object \n",
      " 10  Average Cost for two  9551 non-null   int64  \n",
      " 11  Currency              9551 non-null   object \n",
      " 12  Has Table booking     9551 non-null   object \n",
      " 13  Has Online delivery   9551 non-null   object \n",
      " 14  Is delivering now     9551 non-null   object \n",
      " 15  Switch to order menu  9551 non-null   object \n",
      " 16  Price range           9551 non-null   int64  \n",
      " 17  Aggregate rating      9551 non-null   float64\n",
      " 18  Rating color          9551 non-null   object \n",
      " 19  Rating text           9551 non-null   object \n",
      " 20  Votes                 9551 non-null   int64  \n",
      "dtypes: float64(3), int64(5), object(13)\n",
      "memory usage: 1.5+ MB\n"
     ]
    }
   ],
   "source": [
    "#check dataset information\n",
    "dataset.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "c8fe1296-c2f7-4f2c-8bd6-6bd6c79999c9",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['Restaurant ID', 'Restaurant Name', 'Country Code', 'City', 'Address',\n",
       "       'Locality', 'Locality Verbose', 'Longitude', 'Latitude', 'Cuisines',\n",
       "       'Average Cost for two', 'Currency', 'Has Table booking',\n",
       "       'Has Online delivery', 'Is delivering now', 'Switch to order menu',\n",
       "       'Price range', 'Aggregate rating', 'Rating color', 'Rating text',\n",
       "       'Votes'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#check dataset column names\n",
    "dataset.columns"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "7d93ed8e-58a6-41de-bb60-11480a5cf589",
   "metadata": {},
   "source": [
    "Data preprocessing"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "d6c4f812-ef94-466e-a192-bf6ca6348bc0",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Restaurant ID           0\n",
       "Restaurant Name         0\n",
       "Country Code            0\n",
       "City                    0\n",
       "Address                 0\n",
       "Locality                0\n",
       "Locality Verbose        0\n",
       "Longitude               0\n",
       "Latitude                0\n",
       "Cuisines                9\n",
       "Average Cost for two    0\n",
       "Currency                0\n",
       "Has Table booking       0\n",
       "Has Online delivery     0\n",
       "Is delivering now       0\n",
       "Switch to order menu    0\n",
       "Price range             0\n",
       "Aggregate rating        0\n",
       "Rating color            0\n",
       "Rating text             0\n",
       "Votes                   0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#check for null values\n",
    "pd.isnull(dataset).sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "614963a2-9108-4a15-ab64-326d787d2526",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Drop all null values\n",
    "dataset.dropna(inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "b7fcd561-420a-41f6-bfc3-ddde2eaae18b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(9542, 21)"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#check Database\n",
    "dataset.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "f3d1e195-8406-45b6-8651-c4a6e1087a77",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Index: 9542 entries, 0 to 9550\n",
      "Data columns (total 21 columns):\n",
      " #   Column                Non-Null Count  Dtype  \n",
      "---  ------                --------------  -----  \n",
      " 0   Restaurant ID         9542 non-null   int64  \n",
      " 1   Restaurant Name       9542 non-null   object \n",
      " 2   Country Code          9542 non-null   int64  \n",
      " 3   City                  9542 non-null   object \n",
      " 4   Address               9542 non-null   object \n",
      " 5   Locality              9542 non-null   object \n",
      " 6   Locality Verbose      9542 non-null   object \n",
      " 7   Longitude             9542 non-null   float64\n",
      " 8   Latitude              9542 non-null   float64\n",
      " 9   Cuisines              9542 non-null   object \n",
      " 10  Average Cost for two  9542 non-null   int64  \n",
      " 11  Currency              9542 non-null   object \n",
      " 12  Has Table booking     9542 non-null   object \n",
      " 13  Has Online delivery   9542 non-null   object \n",
      " 14  Is delivering now     9542 non-null   object \n",
      " 15  Switch to order menu  9542 non-null   object \n",
      " 16  Price range           9542 non-null   int64  \n",
      " 17  Aggregate rating      9542 non-null   float64\n",
      " 18  Rating color          9542 non-null   object \n",
      " 19  Rating text           9542 non-null   object \n",
      " 20  Votes                 9542 non-null   int64  \n",
      "dtypes: float64(3), int64(5), object(13)\n",
      "memory usage: 1.6+ MB\n"
     ]
    }
   ],
   "source": [
    "dataset.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "943f6f13-2936-40ff-814f-5fbf334a4c27",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Average Cost for two</th>\n",
       "      <th>Price range</th>\n",
       "      <th>Aggregate rating</th>\n",
       "      <th>Votes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>9542.000000</td>\n",
       "      <td>9542.000000</td>\n",
       "      <td>9542.000000</td>\n",
       "      <td>9542.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>1200.326137</td>\n",
       "      <td>1.804968</td>\n",
       "      <td>2.665238</td>\n",
       "      <td>156.772060</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>16128.743876</td>\n",
       "      <td>0.905563</td>\n",
       "      <td>1.516588</td>\n",
       "      <td>430.203324</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>250.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>2.500000</td>\n",
       "      <td>5.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>400.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>3.200000</td>\n",
       "      <td>31.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>700.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>3.700000</td>\n",
       "      <td>130.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>800000.000000</td>\n",
       "      <td>4.000000</td>\n",
       "      <td>4.900000</td>\n",
       "      <td>10934.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       Average Cost for two  Price range  Aggregate rating         Votes\n",
       "count           9542.000000  9542.000000       9542.000000   9542.000000\n",
       "mean            1200.326137     1.804968          2.665238    156.772060\n",
       "std            16128.743876     0.905563          1.516588    430.203324\n",
       "min                0.000000     1.000000          0.000000      0.000000\n",
       "25%              250.000000     1.000000          2.500000      5.000000\n",
       "50%              400.000000     2.000000          3.200000     31.000000\n",
       "75%              700.000000     2.000000          3.700000    130.000000\n",
       "max           800000.000000     4.000000          4.900000  10934.000000"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#check description \n",
    "dataset[['Average Cost for two', 'Price range', 'Aggregate rating', 'Votes']].describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "1e685f3c-71f1-4712-8579-14f169cfee71",
   "metadata": {},
   "outputs": [],
   "source": [
    "#top three common cuisiness in the dataset\n",
    "cuisine_count = dataset['Cuisines'].str.split(',').explode().str.strip().value_counts()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "f8f32cc7-0d1b-48d3-8e30-4a23c3bb35dd",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Cuisines\n",
      "North Indian    3960\n",
      "Chinese         2735\n",
      "Fast Food       1986\n",
      "Name: count, dtype: int64\n"
     ]
    }
   ],
   "source": [
    "#str.split(',')- split the cuisine in the column into lists\n",
    "#explode()- expand these lists into separate rows\n",
    "#value_counts()- counts thoccurnece of cuisines \n",
    "\n",
    "#determine the top 3 cuisine in the dataset\n",
    "top_three_cuisines = cuisine_count.head(3)\n",
    "print(top_three_cuisines)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "id": "ab4d32f7-0856-4fc9-aa40-3ad452486a87",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Dimpi\\AppData\\Local\\Temp\\ipykernel_7952\\1972996104.py:2: FutureWarning: \n",
      "\n",
      "Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.\n",
      "\n",
      "  sns.barplot(\n"
     ]
    },
    {
     "data": {
      "image/png": "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yMb++ecfw8vLy/D39zfc3d0d9v3111+Gh4eH8fjjjxvLli0zFi5caFSoUMHw9/c3zpw541B25MiRhs1mMwYNGmSsW7fOGD9+vJEnTx7j1VdfdSgXGxtrVKxY0ShatKgxd+5c47///a/RsmVLw9nZ2Vi/fv1ttT06OtqQZERHR2es87gt+fLlMz755BNj7969hiQjMjLS3JeYmGj4+PgYM2fONLfVqlXLCAsLS7e+P//805BkbN682dy2adMmQ5KxZ8+eu9MJAABwT91qXsvWgblFixbGU089Zbz88supAnP79u0NPz8/hw4ePnzYyJ07tzFgwABz27lz5wwXFxeja9euDsePGjXKsNlsxu7du81tU6dONSQZGzduNLclJCQY5cuXN2rWrHlbbScw3xuJiYnGV199ZeTJk8fYvXu38ccffxiSjL///tuhXKFChYyXX37ZMAzDOH36tCHJ+OCDD4w6deoYBQoUMJ544gnjp59+Mst/+umnhpeXV6rzeXl5GbNmzbqbXQIAAPfIrea1bDslY+7cudqwYYOmTZuWal9iYqKWLl2qtm3bytPT09weEBCg+vXra9GiRea2FStWKDY2ViEhIQ51hISEyDAMLV682Ny2aNEilStXTnXq1DG3OTs768UXX9TWrVt1/PjxTOwh7sSuXbuUN29e2e12vf7661q0aJHKly+vwMBABQQEaNCgQbpw4YLi4+M1duxYnTp1SidPnpQkc9rOiBEj9Oqrr2rFihWqVq2aGjZsaM51PnXqlAoUKJDqvAUKFNCpU6fuXUcBAECWy5aB+cyZM+rbt6/Gjh2rokWLptp/4MABXbt2TZUrV061r3Llyvr7778VGxsrSYqMjJQkVapUyaFc4cKF5efnZ+5PLptenZK0e/fujHcKmapcuXLauXOnNm/erG7duunll1/Wn3/+qdy5c2vhwoXat2+ffHx85ObmpvXr16tZs2bKlSuXJCkpKUmS9NprrykkJERVq1bVpEmTVK5cOc2aNcs8h81mS3VewzDS3A4AAO5fzlndgLR0795d5cqVU7du3dLcHxUVJUny8fFJtc/Hx0eGYejChQsqXLiwoqKiZLfb5e7unmbZ5LqS602vzpTnTUtcXJzi4uLMxzExMemWxZ3LkyePypQpI0l6+OGHtW3bNk2ePFkff/yxqlevrp07dyo6Olrx8fHKnz+/atWqpYcffljSjS9LklS+fHmHOh966CEdPXpUklSoUCGdPn061XnPnj2rggUL3s2uAQCAbCbbjTAvXLhQ33//vWbOnPmvI3lW+1Puu9Vyt1s2pTFjxpjLj3l5ealYsWLplkXmMwzD4QuLJHl5eSl//vzav3+/tm/frpYtW0qSSpQoIX9/f+3du9eh/L59+xQQECBJqlOnjqKjo7V161Zz/5YtWxQdHa1HHnnkLvcGAABkJ9lqhPny5cvq0aOHevXqJX9/f3PN2/j4eEnSxYsXlTt3bvn6+kpKe8T3/Pnzstls8vb2liT5+voqNjZWV69elZubW6qy1atXNx/7+vqmW6eU9oh2skGDBql///7m45iYGELzXTJ48GA1a9ZMxYoV06VLl/T1119r/fr1WrFihSRp/vz5yp8/v4oXL65du3apT58+atWqlZo0aSLpxheft956S8OHD1dQUJCqVKmiOXPmaM+ePVqwYIGkG6PNwcHBevXVV/Xxxx9Lkrp27aoWLVqoXLlyWdNxAACQJbJVYD537pxOnz6t9957T++9916q/fny5VPLli21YMECubq6ateuXanK7Nq1S2XKlJGLi4uk/81d3rVrl2rVqmWWO3XqlM6dO6eKFSua2ypVqpRunZIcyt7MbrfLbrffYk9xJ06fPq2OHTvq5MmT8vLyUuXKlbVixQo1btxYknTy5En1799fp0+fVuHChfXSSy9p6NChDnX07dtXsbGx6tevn86fP6+goCCtWrVKpUuXNst88cUX6t27txm0n376aX344Yf3rqMAACBbsBmGYWR1I5LFxsZq8+bNqbaPHTtWGzZs0PLly+Xn56eKFSvq2Wef1fr16/X333/Lw8NDknT06FGVLVtW/fr109ixYyXdGB0uUqSIOnXqpOnTpzvUOXjwYEVGRppzWadPn67u3btr8+bNZrhOTExUlSpVlDdv3jTblp6YmBh5eXkpOjraYSUPAAAAZA+3mteyVWBOT6dOnbRgwQJdvnzZ3LZnzx7VqFFD1apVU2hoqGJjYzVs2DCdP39eO3fuVP78+c2yo0aN0tChQzVo0CA1adJE27ZtU1hYmF566SXNmDHDLBcXF6fq1asrJiZGY8eOVYECBTRt2jR9//33Wr16terWrXvLbSYwAwAAZG+3mtey1ZSM2xEYGKj169dr4MCBateunZydndWgQQNN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tdsOzMlKly7NCDIAAADueyySDAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFjIdoH50qVLGjBggJo0aaL8+fPLZrNpxIgRqcp16tRJNpst1U9gYGCa9U6ZMkWBgYGy2+0qWbKkwsPDlZCQkKrcmTNn1KlTJ/n5+cnNzU116tTRmjVrMrubAAAAyCGcs7oBN4uKitKMGTMUFBSkVq1a6ZNPPkm3rKurq9auXZtq281GjRqloUOHKjQ0VE2aNNG2bdsUFham48ePa8aMGWa5uLg4NWzYUBcvXtTkyZNVoEABTZ06VcHBwVq9erXq1q2beR0FAABAjpDtAnNAQIAuXLggm82mc+fOWQZmJycn1a5d27K+qKgojRw5Uq+++qpGjx4tSapXr54SEhIUFhamvn37qnz58pKkTz/9VJGRkdq4caPq1KkjSapfv76CgoI0YMAAbdmyJZN6CQAAgJwi203JSJ5akVlWrFih2NhYhYSEOGwPCQmRYRhavHixuW3RokUqV66cGZYlydnZWS+++KK2bt2q48ePZ1q7AAAAkDNku8B8O65du6ZChQopV65cKlq0qHr27Knz5887lImMjJQkVapUyWF74cKF5efnZ+5PLlu5cuVU50netnv37szuAgAAALK5bDcl41YFBQUpKChIFStWlCRt2LBBkyZN0po1a7Rt2zblzZtX0o0pGXa7Xe7u7qnq8PHxUVRUlPk4KipKPj4+aZZL3p+euLg4xcXFmY9jYmIy1jEAAABkKzk2MPfr18/hcePGjVW1alW1a9dOM2fOdNhvNcXj5n23UzalMWPGKDw8/N+aDQAAgBwmR0/JuFnr1q3l7u6uzZs3m9t8fX0VGxurq1evpip//vx5hxFlX1/fNEeRk6d5pDX6nGzQoEGKjo42f44dO3YnXQEAAEA2cV8FZkkyDENOTv/rVvLc5V27djmUO3XqlM6dO2dO6Ugue3O5lMemLHszu90uT09Phx8AAADkfPdVYF6wYIGuXr3qsNRccHCwXFxcFBER4VA2IiJCNptNrVq1Mre1bt1ae/bscVg+LjExUXPnzlWtWrXk7+9/t7sAAACAbCZbzmFevny5rly5okuXLkmS/vzzTy1YsECS1Lx5c509e1YdOnTQc889pzJlyshms2nDhg16//33VaFCBXXp0sWsy8fHR2FhYRo6dKh8fHzMG5eMGDFCXbp0MddglqTOnTtr6tSpat++vcaOHasCBQpo2rRp2rt3r1avXn1vfwkAAADIFrJlYO7WrZuOHDliPp4/f77mz58vSTp06JC8vLxUsGBBTZw4UadPn9b169cVEBCg3r17a/DgwalWxBgyZIg8PDw0depUTZgwQYUKFVJoaKiGDBniUM5ut2vNmjUaMGCAevXqpatXr6pKlSpavnw5d/kDAAB4QGXLwHz48OF/LfPtt9/eVp29e/dW7969/7VcwYIFNWfOnNuqGwAAAPev+2oOMwAAAJDZCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACABQIzAAAAYIHADAAAAFggMAMAAAAWCMwAAACA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03T27NmsajaQrdx8iVny44oVK+rgwYOaNWuWEhMTzc8TSbp48aLq1aun/v37q169eve6yfc1LvoDMonV8lhz5szR4MGD5e7urk8++URPPPGEDMMwV9CIiopSYmKiChYseI9bDWSulHP34+LiZLfbJUkrVqzQk08+qT59+ujzzz9Xw4YNNXPmTHl4eOjMmTMaOHCgTp06pblz58rX1zcruwBkuZSvI8MwFBsbK2dnZ+XOnVvnzp1TjRo15OTkpFGjRum5556TJEVFRal///4qWbKkBg4cyPKlmYzADGSClG9ux44d05UrV2S321WyZEmzzCeffKKRI0fKxcVFM2bMSBWagZwu5etg8ODBOnXqlMaPHy8/Pz/9888/6tq1q1avXq0KFSrot99+k3RjaayRI0fqhx9+0Lp161S+fPms7AKQ5VK+jkaPHq0dO3Zoz549qly5sjp27KhmzZrpjz/+0JNPPqnz58/r8ccfV9myZfX777/r999/1+bNm/XQQw9lcS/uPwRm4A6lfHPr06ePNm/erIMHD0q6cTVzmzZt5O3tLelGaH7nnXfk4eGhyZMnq2HDhlnVbCBTpfwLyzPPPKNdu3apWbNm6tWrl/nF8ZdfftGQIUO0ceNGtWjRQk5OToqKitL+/fu1dOlSValSJQt7AGS9lKtatG3bVps2bVLVqlXl5OSkTZs26fz585o+fbpee+01nTx5Um+99ZZ27typuLg4lS5dWhMmTFDFihWzuBf3JwIzcAdSvrk999xz2rx5s8LDw1W5cmW99tpr+u233zRixAj16NHDDM2zZs1Snz599NBDD2nDhg1ycXHhSmbcN7p27ao1a9bo888/V5UqVeTm5uYwNePw4cNaunSplixZInd3d9WqVUvPPvssq2QAKYwePVpTpkzRwoULVb16ddntdm3YsEHvvfeeli5dqgULFqhNmza6fv26rl27poSEBLm4uDAN4y5iWTkgA5JH05KD7rBhw/T777/ryy+/1COPPKIJEyYoMjJSTZs21bBhwyRJ3bp1k4+Pjzp37qzcuXOrdu3avLnhvrJr1y6tXbtWYWFheuSRRyRJR48e1fvvv68TJ06oSpUq6tSpk3r27KmePXtmcWuB7CkhIUHbt29XzZo1VatWLXN73bp1ZbfbtXfvXo0ZM0b169dXvnz5uFPmPcIqGcBtuHLliv755x+H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",
      "text/plain": [
       "<Figure size 800x800 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "fig, Ax= plt.subplots(figsize=(8,8))\n",
    "sns.barplot(\n",
    "    x=top_three_cuisines.index,\n",
    "    y=top_three_cuisines.values,\n",
    "    ax=Ax,\n",
    "    palette=\"rocket\",\n",
    ")\n",
    "for i,value in enumerate(top_three_cuisines.values):\n",
    "    Ax.text(i,value + 15,  #add offset above bar\n",
    "            f'{value}',   #display count\n",
    "            ha=\"center\",\n",
    "            fontsize=10,\n",
    "            color='black')\n",
    "plt.title('Top Three Most Common Cuisines', fontsize=18)\n",
    "plt.xlabel('Cuisine', fontsize=14)\n",
    "plt.ylabel('Count', fontsize=14)\n",
    "plt.xticks(rotation=45, fontsize=12)\n",
    "plt.yticks(fontsize=12)\n",
    "plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "00a54743-8499-409e-9e7e-7176085b1fa3",
   "metadata": {},
   "source": [
    "1:2 CALCULATE THE PERCENTAGE OF RESTAURANTS THAT SERVE EACH OF THE TOP CUISINES."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "id": "383a0fa2-216b-4dad-af56-89c7976b6cda",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "        Cuisine  Count  Percentage (%)\n",
      "0  North Indian   3960           41.50\n",
      "1       Chinese   2735           28.66\n",
      "2     Fast Food   1986           20.81\n"
     ]
    }
   ],
   "source": [
    "#calculate the percentage\n",
    "total_restaurants = len(dataset)\n",
    "top_cuisines_percentage = (top_three_cuisines/ total_restaurants * 100).round(2)\n",
    "\n",
    "#combine result into a dataframe\n",
    "top_cuisines_dataset= pd.DataFrame({\n",
    "    'Cuisine': top_three_cuisines.index,\n",
    "    'Count': top_three_cuisines.values,\n",
    "    'Percentage (%)': top_cuisines_percentage.values\n",
    "})\n",
    "\n",
    "print(top_cuisines_dataset)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "b1a88698-664e-468a-877d-86ddde5163d0",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Dimpi\\AppData\\Local\\Temp\\ipykernel_7952\\1127148451.py:2: FutureWarning: \n",
      "\n",
      "Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.\n",
      "\n",
      "  ab=sns.barplot(x=top_cuisines_percentage.index, y=top_cuisines_percentage.values, palette=\"rocket\")\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "Text(0.5, 1.0, 'Percentage of Restasurants Serving Top Three Cuisines')"
      ]
     },
     "execution_count": 41,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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LvY5lt/PlJUrVyo2NlalS5eWr6+vypcvry5duuivv/664D6DZxT+//bD43Le2MqUKSNJ6tu3r2bOnKmBAwdq3LhxOnDggEaNGqVGjRrp+++/V0hIiOuxaWlpuvfee/Xkk09q7NixKlKkiI4cOaImTZooNTVVTz31lOrXr6+jR48qOTlZaWlpqlatmk6fPq2OHTvqyy+/1JNPPqlGjRpp586dGjFihGJjY7V+/Xr5+vq61vP9999r6NChevrppxUSEqK33npLDzzwgCpVqqSmTZuqXbt2Gjt2rJ555hlNnTpVderUkfT/T639+uuvatiwoR588EEFBQUpNTVVEydOVJMmTbR582Z5eXlJ+vuoSefOndW0aVPNmzdP2dnZmjBhQq6gVtD9dLbVq1erZcuWiomJ0dtvvy2n06lp06apQ4cOev/999WtWzc9+OCDqlWrltvpuvwehTrTjh07JElVqlRxtaWnp+vmm29WkSJF9Pzzz6tixYpau3atRo8erdTUVCUlJUmS5s6dq379+mnAgAGaMGGCihQpou3bt+unn36SJI/t9549e+rbb7/VmDFjVKVKFR06dEjffvutK3hdjGHDhqlhw4Z6/fXXVaRIEQUHB7s+dEaMGKHQ0FAdPXpUCxYsUGxsrFasWJHrw3Hq1KmqVq2aJk2aJEl67rnn1LZtW+3YsUNBQUF67rnnlJmZqQ8//FBr1651PS4sLExr165Vt27d1K1bNyUkJMjHx0c7d+7UypUrz1t33bp15eXlpUGDBun555/XrbfemmfwzO/fMcfkyZNVpUoVTZgwQYGBgapcubLat2+vWbNmaeTIkW5BNikpSd7e3hc823Hy5EndfvvteuCBBzR06FAlJyfrhRdeUFBQkJ5//nlJf1+D2rx5cx04cEDjxo1TpUqVtGTJEnXr1u28Y+eHMUadOnXSihUrNGzYMN1yyy3atGmTRowYobVr12rt2rVur5uNGzdq8ODBSkhIUGhoqN577z0NGjRIJ06c0OOPP37J9eRIT09Xjx49NHToUI0YMUILFizQsGHDVLZsWfXq1cut77meq7Nnz1avXr3UsWNHzZo1S15eXnrjjTfUunVrLV261HWm46efflKjRo1Uvnx5vfzyywoNDdXSpUs1cOBA/fnnnxoxYkSeNeZcy92pUyePbXdeLvRecj75eY7l9zMlNTVV7dq10y233KJ33nlHJUqU0B9//KElS5boxIkTnJm7XAz+sZKSkowks27dOnPy5Elz5MgR8+mnn5oyZcqYgIAAk56ebtauXWskmZdfftntsbt37za+vr7mySefdLU1a9bMSDIrVqxw6ztq1CgjySxfvjzPWt5//30jycyfP9+tPSUlxUgy06ZNc7VFRkYaHx8fs3PnTlfbsWPHTKlSpUzfvn1dbf/+97+NJPPFF1+cdz+cPn3anDx50uzcudNIMh9//LFrWb169UxERITJyspytR05csSULl3anPnyKMh+OpcGDRqY4OBgc+TIEVdbdna2iY6ONuHh4eb06dPGGGN27NhhJJmXXnrpvOOd2XfcuHHm5MmT5vjx42bjxo2mYcOGJiwszOzYscPVt2/fvsbf399tnxpjzIQJE4wk8+OPPxpjjOnfv78pUaLEedfrif3u7+9vBg8efN7HR0ZGmt69e+dqb9asmWnWrJlr/osvvjCSTNOmTc87njF/7/OTJ0+aFi1amDvuuMPVnrMva9asabKzs13t33zzjZFk3n//fVdbfHy8OddbZ86+PHTo0AXrONvbb79t/P39jSQjyYSFhZlevXqZ5ORkt375/TvmbE/FihXNiRMn3PouWrTISDLLli1z2y9ly5Y1Xbp0cbXl7Ncz/869e/c2kswHH3zgNmbbtm1N1apVXfNTp041ksznn3+eq35JJikpKd/7ZsSIEUaS2bdvnzHGmCVLlhhJZvz48W795s2bZySZN99809UWGRlpHA6H2bhxo1vfli1bmsDAQJOZmZmvGi70usx5b/z666/d2m+44QbTunVr13xez9XMzExTqlQp06FDB7f2U6dOmVq1apmbb77Z1da6dWsTHh5uDh8+7Na3f//+xsfHxxw4cCDP7XjkkUeMJPPzzz+ff4P/T86+P1vOZ8uZ7zFnvy7z815yKc+x/H6mfPjhh0ZSrucALi9Oo18DGjRoIC8vLwUEBKh9+/YKDQ3V559/rpCQEH366adyOBy69957lZ2d7ZpCQ0NVq1atXHcJlixZMtfpl88//1xVqlTRbbfdlmcNn376qUqUKKEOHTq4rad27doKDQ3NtZ7atWu7TuVIko+Pj6pUqeI69X8he/fu1SOPPKKIiAgVK1ZMXl5eioyMlCRt2bJF0t9HX9avX69OnTrJ29vb9Vh/f3916NAhV/0F2U9nyszM1Ndff62uXbvK39/f1V60aFH17NlTv//+u7Zu3Zqv7TqXp556Sl5eXvLx8VHt2rX1ww8/6JNPPnE7Bf/pp5+qefPmKlu2rFv9cXFxkuS6A/Xmm2/WoUOHdM899+jjjz8+52UH55Of/Z6znpkzZ2r06NFat26dTp48edHbn6NLly7nbH/99ddVp04d+fj4uGpasWKFWz052rVrp6JFi7rmY2JiJClfz7t69epJku666y598MEHBfrGh/vvv1+///675syZo4EDByoiIkKzZ89Ws2bN9NJLL7n65ffvmOP22293HU3OERcXp9DQULejoEuXLtWePXsueMpf+vvygbNfHzExMW77aPXq1QoICHC7yUaS7rnnnguOfyE5R4rPvsTizjvvlJ+fX67TzjVq1Mh1s0v37t2VkZGhb7/99pLryREaGuq6uSvH2fslx9nP1TVr1ujAgQPq3bu329/19OnTatOmjVJSUpSZmanjx49rxYoVuuOOO1S8eHG3vm3bttXx48fdLvu4ki7lvSQ/z7H8fqbUrl1b3t7eevjhhzVr1qx8X/YEzyJsXgPeffddpaSk6LvvvtOePXu0adMmNW7cWNLf1/UZYxQSEiIvLy+3ad26dbneIM51em/fvn1uF9Ofy//+9z8dOnRI3t7eudaTnp6eaz2lS5fONYbT6dSxY8cuuL2nT59Wq1at9NFHH+nJJ5/UihUr9M0337jehHPGOHjwoGvbz3Z2W0H305ly1nOufVe2bFlJuqTTx4MGDVJKSoq++uorTZgwQSdPnlTHjh3dxvzf//6nTz75JFftNWrUkCRX/T179tQ777yjnTt3qkuXLgoODlb9+vW1fPnyC9aR3/0uSfPmzVPv3r311ltvqWHDhipVqpR69eql9PT0i94P59q/EydO1KOPPqr69etr/vz5WrdunVJSUtSmTZtzPpfOft7lnI7Nz/OuadOmWrhwobKzs9WrVy+Fh4crOjpa77//fr7qDwoK0j333KNXX31VX3/9tTZt2qSQkBANHz7cdS1ifv+O59snxYoVU8+ePbVgwQLXuDNnzlRYWJhat259wTqLFy8uHx8ftzan06njx4+75vfv35+v19XF2L9/v4oVK+a6DCiHw+FQaGhortdSaGhorjFy2i7ldXe2grxnnf13yblsp2vXrrn+tuPGjZMxRgcOHND+/fuVnZ2t1157LVe/tm3bSsr9HDhTzn/gcy61selS3kvy8xzL72dKxYoV9Z///EfBwcGKj49XxYoVVbFiRb366que3WCcF9dsXgOqV6/uumnkbNddd50cDoe+/PLLc14feHbbuS4WL1OmjH7//ffz1nDdddepdOnSrjtLzxYQEHDexxfEDz/8oO+//14zZ85U7969Xe0516rmKFmypBwOxzmvzzw79BR0P529niJFiigtLS3Xsj179rjGv1jh4eGuv2/jxo0VGhqqe++9VyNGjNCUKVNc48fExGjMmDHnHCMn9ErSfffdp/vuu0+ZmZlKTk7WiBEj1L59e/3yyy+uo5Tnkt/9nlPPpEmTNGnSJO3atUuLFi3S008/rb1797qeIz4+PrluCJD+/jA91/4613Nz9uzZio2N1fTp093ajxw5kud2XIqOHTuqY8eOysrK0rp165SYmKju3burQoUKatiwYYHGqlGjhu6++25NmjRJv/zyi26++eYC/R2lc+8T6e+/8UsvvaS5c+eqW7duWrRokQYPHux2VPdSlC5dWt98802u9kv5z8SZY2dnZ2vfvn1ugdMYo/T0dNcR5vOtM6ftXAHxcjj775LzfH7ttdfyvDs7JCRE2dnZrjMi8fHx5+wXFRWV53pbt26tZ555RgsXLsx11PlccgJfVlaW23tcfo9SXux7SX4U5DPllltu0S233KJTp05p/fr1eu211zR48GCFhITo7rvvvqQ6kD+EzWtc+/bt9eKLL+qPP/7QXXfddVFjxMXF6fnnn9fKlSvzvMOxffv2mjt3rk6dOqX69etfSskueR11ynkjPzsAvvHGG27zfn5+qlu3rhYuXKgJEya4TqUfPXpUn376aa76L3Y/+fn5qX79+vroo480YcIE141Qp0+f1uzZsxUeHu52M8+l6tGjh9566y3NmDFDTzzxhCIjI9W+fXstXrxYFStWzPfXmvj5+SkuLk4nTpxQp06d9OOPPyoyMvKS9/vZypcvr/79+2vFihX673//62qvUKGCNm3a5Nb3l19+0datW/Mdzh0OR656Nm3apLVr1yoiIiJfY5ztzO0/86a2s/s0a9ZMJUqU0NKlS/Xdd9/lGTb379+vgIAAt0s5cuR8m0NOiLyYv+O5VK9eXfXr11dSUpJOnTqlrKwst69dulTNmjXTBx98oM8//9x1il/6+6aRS9WiRQuNHz9es2fP1mOPPeZqnz9/vjIzM3N9ZdiPP/6o77//3u1U+pw5cxQQEOC6we1Ka9y4sUqUKKGffvpJ/fv3z7Oft7e3mjdvru+++04xMTHnfM6cT506dRQXF6e3335bd9111znfr9evX6/g4GCVL1/edSnOpk2b3EL8J598UqD15vVeciku5jOlaNGiql+/vqpVq6b33ntP3377LWHzMiFsXuMaN26shx9+WPfdd5/Wr1+vpk2bys/PT2lpafrqq69Us2ZNPfroo+cdY/DgwZo3b546duyop59+WjfffLOOHTum1atXq3379mrevLnuvvtuvffee2rbtq0GDRqkm2++WV5eXvr999/1xRdfqGPHjrrjjjsKVHvOL3a8+eabCggIkI+Pj6KiolStWjVVrFhRTz/9tIwxKlWqlD755JNznr4ZNWqU2rVrp9atW2vQoEE6deqUXnrpJfn7++vAgQMe20+JiYlq2bKlmjdvrscff1ze3t6aNm2afvjhB73//vt5HoG6WOPGjVP9+vX1wgsv6K233tKoUaO0fPlyNWrUSAMHDlTVqlV1/PhxpaamavHixXr99dcVHh6uhx56SL6+vmrcuLHCwsKUnp6uxMREBQUFuT5sLnW/Hz58WM2bN1f37t1VrVo1BQQEKCUlxfXNADl69uype++9V/369VOXLl20c+dOjR8/Ptfp0/Np3769XnjhBY0YMULNmjXT1q1bNWrUKEVFReX6yqf8qlmzpmsfx8XFqWjRooqJidHo0aP1+++/q0WLFgoPD9ehQ4f06quvysvL67xfyv7FF19o0KBB6tGjhxo1aqTSpUtr7969ev/997VkyRLXKXlJ+f475sf999+vvn37as+ePWrUqNEFfzygIHr37q1XXnlF9957r0aPHq1KlSrp888/19KlSyXl/jqngmjZsqVat26tp556ShkZGWrcuLHrbvQbb7xRPXv2dOtftmxZ3X777UpISFBYWJhmz56t5cuXa9y4cYXmTmR/f3+99tpr6t27tw4cOKCuXbu6vk3h+++/1759+1xH51999VU1adJEt9xyix599FFVqFBBR44c0fbt2/XJJ59c8NsP3n33XbVp00ZxcXG6//77FRcXp5IlSyotLU2ffPKJ3n//fW3YsEHly5dX27ZtVapUKT3wwAMaNWqUihUrppkzZ2r37t0X3Kb8vJdcivx+prz++utauXKl2rVrp/Lly+v48eOur9E7330G8LArd28SbMu5YzAlJeWCfd955x1Tv3594+fnZ3x9fU3FihVNr169zPr16119mjVrZmrUqHHOxx88eNAMGjTIlC9f3nh5eZng4GDTrl07t7seT548aSZMmGBq1aplfHx8jL+/v6lWrZrp27ev2bZtm6tfZGSkadeuXa51nH23ozHGTJo0yURFRZmiRYu63eX6008/mZYtW5qAgABTsmRJc+edd5pdu3YZSWbEiBFuYyxYsMDUrFnTeHt7m/Lly5sXX3zRDBw40JQsWfKi9lNevvzyS3Prrbe6HtugQQPzySefuPW5mLvR8+p75513mmLFipnt27cbY4zZt2+fGThwoImKijJeXl6mVKlS5qabbjLDhw83R48eNcYYM2vWLNO8eXMTEhJivL29TdmyZc1dd91lNm3a5Db2pez348ePm0ceecTExMSYwMBA4+vra6pWrWpGjBjhdnfw6dOnzfjx4831119vfHx8TN26dc3KlSvzvBv93//+d659kJWVZR5//HFTrlw54+PjY+rUqWMWLlxoevfubSIjI/O1L89+zmRlZZkHH3zQlClTxjgcDtdduZ9++qmJi4sz5cqVM97e3iY4ONi0bdvWfPnll3n+DY35+xsNnn32WdO4cWMTGhpqihUrZgICAkz9+vXNa6+95nZ3fH7/jvl5Hh0+fNj4+voaSWbGjBm5lud1p7Cfn1+uvue6a3nXrl2mc+fOxt/f3wQEBJguXbqYxYsX5/pmggs5+250Y/7+doqnnnrKREZGGi8vLxMWFmYeffRRc/DgQbfH5ryXfPjhh6ZGjRrG29vbVKhQwUycODHf6zcmf3ejn+u98ezn2fmeq8YYs3r1atOuXTtTqlQp4+XlZcqVK2fatWuXq/+OHTvM/fffb8qVK2e8vLxMmTJlTKNGjczo0aPztT3Hjh0zkydPNg0bNjSBgYGmWLFipmzZsqZz587ms88+c+v7zTffmEaNGhk/Pz9Trlw5M2LECPPWW29d8G70/LyXXOpzLD+fKWvXrjV33HGHiYyMNE6n05QuXdo0a9bMLFq0KF/7Cp7hMMaYyxlugcLu5MmTql27tsqVK2f1N8aBa83YsWP17LPPateuXfk+AnspKlSooOjo6FyXxQC4vDiNjmveAw88oJYtW7pO9bz++uvasmULdysClyDn5rRq1arp5MmTWrlypSZPnqx77733sgRNAIUHYRPXvCNHjujxxx/Xvn375OXlpTp16mjx4sVczwNcguLFi+uVV15RamqqsrKyVL58eT311FN69tlnr3RpAC4zTqMDAADAGr7UHQAAANYQNgEAAGANYRMAAADWFLobhE6fPq09e/YoICDA4190DQAAgEtnjNGRI0dUtmzZC/5QQ6ELm3v27Lnon5EDAADA5bN79+4Lfp1ZoQubAQEBkv4uPjAw8ApXAwAAgLNlZGQoIiLCldvOp9CFzZxT54GBgYRNAACAQiw/lzxygxAAAACsIWwCAADAGsImAAAArCFsQpKUmJgoh8OhwYMHu9o++ugjtW7dWtddd50cDoc2btx4wXFmzpwph8ORazp+/Li94gEAQKFF2IRSUlL05ptvKiYmxq09MzNTjRs31osvvlig8QIDA5WWluY2+fj4eLJkAABwlSh0d6Pj8jp69Kh69OihGTNmaPTo0W7LevbsKUlKTU0t0JgOh0OhoaGeKhEAAFzFOLJ5jYuPj1e7du102223eWzMo0ePKjIyUuHh4Wrfvr2+++47j40NAACuLhzZvIbNnTtX3377rVJSUjw2ZrVq1TRz5kzVrFlTGRkZevXVV9W4cWN9//33qly5ssfWAwAArg6EzWvU7t27NWjQIC1btsyj11M2aNBADRo0cM03btxYderU0WuvvabJkyd7bD0AAODqQNi8Rm3YsEF79+7VTTfd5Go7deqUkpOTNWXKFGVlZalo0aKXvJ4iRYqoXr162rZt2yWPBQAArj6EzWtUixYttHnzZre2++67T9WqVdNTTz3lkaApScYYbdy4UTVr1vTIeAAA4OpC2LxGBQQEKDo62q3Nz89PpUuXdrUfOHBAu3bt0p49eyRJW7dulSSFhoa67jbv1auXypUrp8TEREnSyJEj1aBBA1WuXFkZGRmaPHmyNm7cqKlTp16uTQMAAIUId6MjT4sWLdKNN96odu3aSZLuvvtu3XjjjXr99dddfXbt2qW0tDTX/KFDh/Twww+revXqatWqlf744w8lJyfr5ptvvuz1AwCAK89hjDFXuogzZWRkKCgoSIcPH1ZgYOCVLgcAAABnKUhe48gmAAAArCFsAgAAwBrCJgAAAKwhbAIAAMAawiYAAACsIWwCAADAGsImAAAArCFsAgAAwBrC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CJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrrIXNadOmKSoqSj4+Prrpppv05Zdf2loVAAAACikrYXPevHkaPHiwhg8fru+++0633HKL4uLitGvXLhurAwAAQCFlJWxOnDhRDzzwgB588EFVr15dkyZNUkREhKZPn25jdQAAACikinl6wBMnTmjDhg16+umn3dpbtWqlNWvW5OqflZWlrKws1/zhw4clSRkZGR6t6+Spkx4dD7hUnn6O2/IXrx0UMlfDa+fI8awLdwIuM0++dnLGMsZcsK/Hw+aff/6pU6dOKSQkxK09JCRE6enpufonJiZq5MiRudojIiI8XRpQqHwYFHSlSwCuTkHzr3QFwNXp6akeH/LIkSMKusDnmcfDZg6Hw+E2b4zJ1SZJw4YN05AhQ1zzp0+f1oEDB1S6dOlz9seVlZGRoYiICO3evVuBgYFXuhzgqsDrBrg4vHYKL2OMjhw5orJly16wr8fD5nXXXaeiRYvmOoq5d+/eXEc7JcnpdMrpdLq1lShRwtNlwcMCAwN54QMFxOsGuDi8dgqnCx3RzOHxG4S8vb110003afny5W7ty5cvV6NGjTy9OgAAABRiVk6jDxkyRD179lTdunXVsGFDvfnmm9q1a5ceeeQRG6sDAABAIWUlbHbr1k379+/XqFGjlJaWpujoaC1evFiRkZE2VofLyOl0asSIEbkufQCQN143wMXhtfPP4DD5uWcdAAAAuAj8NjoAAACsIWwCAADAGsImAAAArCFs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P61y5cq5Tp1f6DMz5zKVhx56SG+++aaKFSumwYMHy9fX1wN7CRJHNgu9F154Iddpgjp16uiDDz7Q3LlzFR0dreeff16jRo264NdGFCtWTJMnT9Ybb7yhsmXL5rqGxbaXXnpJTZs21e23367bbrtNTZo00U033ZRn/9q1a2vixIkaN26coqOj9d57713wK6GAixEVFaVvv/1WzZs319ChQxUdHa2WLVtqxYoVbtepedqDDz6ot956SzNnzlTNmjXVrFkzzZw503Vk09/fX+PGjVPdunVVr149paamavHixSpSpIgcDocWL16spk2b6v7771eVKlV09913KzU1VSEhIdZqBnLk5z361KlTio+PV/Xq1dWmTRtVrVrVFfLKlSunkSNH6umnn1ZISIj69+9/UXUkJSXppptuUvv27dWwYUMZY7R48WLXZSz5+cxMSkpSRESEmjVrps6dO7u+Ugye4TBc3AYAAABLOLIJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQCXYNWqVXI4HPn6HeWC9AWAfwrCJoBrWnp6ugYMGKDrr79eTqdTERER6tChg1asWJGvxzdq1EhpaWkKCgryaF8A+Kfg5yoBXLNSU1PVuHFjlShRQiNHjlRMTIxOnjyppUuX6s0339TPP/98pUsEgKseRzYBXLP69esnh8Ohb775Rl27dlWVKlVUo0YNDRkyROvWrVNqaqocDoc2btzoesyhQ4fkcDi0atUqSblPje/cuVMdOnRQyZIl5efnpxo1amjx4sXn7Dtz5kyVKFFCS5cuVfXq1eXv7682bdooLS3Nrc6kpCRVr15dPj4+qlatmqZNm+ZaduLECfXv319hYWHy8fFRhQoVlJiYaG2fAUBBFbvSBQDAlXDgwAEtWbJEY8aMkZ+fX67lJUqUuKhrK+Pj43XixAklJyfLz89PP/30k/z9/fPs/9dff2nChAn617/+pSJFiujee+/V448/rvfee0+SNGPGDI0YMUJTpkzRjTfeqO+++04PPfSQ/Pz81Lt3b02ePFmLFi3SBx98oPLly2v37t3avXt3gesGAFsImwCuSdu3b5cxRtWqVfPouLt27VKXLl1Us2ZNSdL1119/3v4nT57U66+/rooVK0qS+vfvr1GjRrmWv/DCC3r55ZfVuXNnSVJUVJR++uknvfHGG+rdu7d27dqlypUrq0mTJnI4HIqMjPTo9gDApeI0OoBrUs7l6g6Hw6PjDhw4UKNHj1bjxo01YsQIbdq06bz9ixcv7gqakhQWFqa9e/dKkvbt26fdu3frgQcekL+/v2saPXq0fv31V0lSnz59tHHjRlWtWlUDBw7UsmXLPLo9AHCpCJsArkmVK1eWw+HQli1b8uxTpMjfb5Fn3kd58uTJ84774IMP6rffflPPnj21efNm1a1bV6+99lqe/b28vNzmHQ6Ha32nT5+W9Pep9I0bN7qmH374QevWrZMk1alTRzt27NALL7ygY8eO6a677lLXrl3PWyMAXE6ETQDXpFKlSql169aaOnWqMjMzcy0/dOiQypQpI0luN+ycebNQXiIiIvTII4/oo48+0tChQzVjxoyLqjEkJETlypXTb7/9pkqVKrlNUVFRrn6BgYHq1q2bZsyYoXnz5mn+/Pk6cODARa0TADyNazYBXLOmTZumRo0a6eabb9aoUaMUExOj7OxsLV++XNOnT9eWLVvUoEEDvfjii6pQoYL+/PNPPfvss+cdc/DgwYqLi1OVKlV08OBBrVy5UtWrV7/oGhMSEjRw4EAFBgYqLi5OWVlZWr9+vQ4ePKghQ4bolVdeUVhYmGrXrq0iRYro3//+t0JDQ1WiRImLXicAeBJhE8A1KyoqSt9++63GjBmjoUOHKi0tTWXKlNFNN92k6dOnS5Leeecd3X///apbt66qVq2q8ePHq1WrVnmOeerUKcXHx+v3339XYGCg2rRpo1deeeWia3zwwQdVvHhxvfTSS3ryySfl5+enmjVravDgwZIkf39/jRs3Ttu2bVPRokVVr149LV682HUJAABcaXypOwAAAKzhv74AAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALCGsAkAAABrCJsAAACwhrAJAAAAawibAAAAsIawCQAAAGsImwAAALDm/wEYtieN51cnTQAAAABJRU5ErkJggg==",
      "text/plain": [
       "<Figure size 800x800 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "fig,ax = plt.subplots(figsize=(8,8))\n",
    "ab=sns.barplot(x=top_cuisines_percentage.index, y=top_cuisines_percentage.values, palette=\"rocket\")\n",
    "for i, value in enumerate(top_cuisines_percentage.values):\n",
    "    ax.text(i, value + 1,  # add offset above bar\n",
    "            f'{value}',  # display count\n",
    "            ha='center',\n",
    "            fontsize=10,\n",
    "            color='black'\n",
    "        )\n",
    "plt.title('Percentage of Restasurants Serving Top Three Cuisines')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "b5871b65-ce22-4d67-bb56-12fc99bc12ec",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.12.7"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
