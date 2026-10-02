# 🔬 Pathway Explorer

### Chemical Reaction Knowledge Graph (USPTO 1976)

*Built for SER 531 at Arizona State University.*

Pathway Explorer is a web-based platform for exploring **chemical
reaction pathways**,\
**searching compounds**, **browsing reactions**, and analyzing
**reaction networks** derived from\
USPTO patent chemistry data.

It is backed by a **GraphDB RDF knowledge graph**, queried with
**SPARQL**, and presented through\
a modern **React + TypeScript** frontend.

------------------------------------------------------------------------

## 🚀 Features

### 🔄 Pathway Discovery

-   Find **1--N step synthetic routes** between compounds\
-   Supports **multiple start** and **multiple target** compounds\
-   Configurable **maximum step depth**\
-   Shows intermediates and reaction IDs step-by-step

### 🔬 Reaction Explorer

-   Search reactions by free-text or compound\
-   View all participants:
    -   Reactants\
    -   Products\
    -   Agents\
    -   Solvents\
    -   Catalysts\
-   Includes linked **patent provenance** and **reaction SMILES**

### 🧪 Compound Explorer

-   Search compounds by SMILES or name\
-   View:
    -   SMILES + label\
    -   Role counts (reactant, product, solvent, catalyst, agent)\
    -   All reactions involving the compound\
-   Useful for understanding compound behavior across many reactions

### 🧠 Knowledge Graph Backend

-   Built entirely on **GraphDB Free Edition**\
-   Custom **OWL ontology** defines reactions, compounds, patents, and
    roles\
-   All features powered by **SPARQL 1.1**

------------------------------------------------------------------------

# 🧬 Data Source & Pipeline

### Dataset

USPTO **1976 chemical grant** patents (CML format).\
Each reaction entry provides: - reaction SMILES\
- reactants, products, solvents, catalysts, agents\
- patent document ID

### Pipeline (ETL)

1.  Parse USPTO CML XML files\
2.  Extract reaction participants\
3.  Normalize SMILES (RDKit canonicalization, atom-map removal)\
4.  Generate RDF triples using `ontology.owl`\
5.  Export graph as `uspto_1976_chemkg.ttl`\
6.  Import into GraphDB

Resulting graph: - \~18,000 reactions\
- \~26,000 compounds\
- \~260,000 triples

------------------------------------------------------------------------

# ⚙️ Technology Stack

-   **React + TypeScript**
-   **TailwindCSS + shadcn/ui**
-   **GraphDB Free Edition**
-   **SPARQL 1.1**
-   **RDF / OWL Ontology**
-   **Python ETL tools**
-   **RDKit (cheminformatics)**

------------------------------------------------------------------------

# 🛠️ Installation & Setup

Follow these steps to run the project locally.

------------------------------------------------------------------------

## 1️⃣ Clone the Repository

``` bash
git clone https://github.com/ShrinidhiMane/ser-531.git
cd ser-531
```

## 2️⃣ Install Frontend Dependencies

``` bash
npm install
npm run dev
```

Frontend: http://localhost:5173

## 3️⃣ Install & Run GraphDB

Download: https://www.ontotext.com/products/graphdb/

Start: - Windows: `graphdb.exe` - macOS/Linux: `bin/graphdb`

Workbench: http://localhost:7200

## 4️⃣ Create a GraphDB Repository

Repository ID: `chemkg`\
Ruleset: `OWL2-RL`

## 5️⃣ Import Data

Upload: - `ontology.owl` - `uspto_1976_chemkg.ttl`

Should contain \~260,000 triples.

## 6️⃣ Configure Frontend → GraphDB Connection

Edit: `src/services/graphdbClient.ts`

Set:

``` ts
const GRAPHDB_BASE_URL = "http://localhost:7200";
const REPOSITORY_ID = "chemkg";
```

------------------------------------------------------------------------

# 🧪 Using the Application

### 🔍 Compound Search

SMILES or name → view compound details.

### 🔬 Reaction Explorer

Browse reactions, participants, SMILES, patent links.

### 🔄 Pathway Explorer

Enter start + target compounds + max steps → get pathways.

------------------------------------------------------------------------

# 🧠 Troubleshooting

❌ No results?\
Both files must be imported into the same repo.

❌ SPARQL errors?\
Likely unescaped SMILES.

❌ Slow search?\
Use `searchService.ts`.

------------------------------------------------------------------------

# 🌱 Future Work

-   Add USPTO applications (2001--2016)\
-   More grant years\
-   Integrate PubChemRDF & ChEMBL-RDF\
-   Add reaction conditions\
-   Pathway ranking & cost metrics\
-   Graph visualization (force layout)

------------------------------------------------------------------------

# 🙏 Acknowledgements

USPTO datasets, RDKit, Ontotext GraphDB, React ecosystem
