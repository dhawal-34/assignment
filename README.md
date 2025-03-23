## Follow these steps to set up and run the project.

### **1. Clone the Repository**

```bash
git clone https://github.com/dhawal-34/assignment
cd assignment
```

---

### **2. Install Python (if not installed)**

Ensure you have **Python 3.12.4** installed. You can check your version with:

```bash
python --version
```

---

### **3. Create a Virtual Environment**

```bash
python -m venv envanalysis
```

Activate the virtual environment:

- **Windows (cmd):**
  ```powershell
  .\envanalysis\Scripts\activate
  ```
- **Mac/Linux:**
  ```bash
  source venv/bin/activate
  ```

---

### **4. Install Dependencies**

Install all required packages using `pip` and the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

---

### **5. Launch Jupyter Notebook**

```bash
jupyter notebook
```

Then open the `analysis.ipynb` file from the **notebook** directory.

## Python Libraries Used
- **Pandas**: For data manipulation and analysis
- **NumPy**: For numerical computations
- **Jupyter Notebook**: For interactive data exploration

## Assignment

### How many finance lending and blockchain clients does the organization have?
- **Number of Finance Lending clients:** 22 
- **Number of Blockchain clients:** 25

### Which industry in the organization has the highest renewal rate?
- **Industry with the highest renewal rate:** Gaming

### What was the average inflation rate when their subscriptions were renewed?
- **Average inflation rate when their subscriptions were renewed:** 4.44

### What is the median amount paid each year for all payment methods?
- **Median amount paid each year for all payment methods:**

| year | amount_paid |
| :----: | :-------: |
| 2018 |  235.7  |
| 2019 |  360.9  |
| 2020 |  284.5  |
| 2021 |  306.8  |
| 2022 |  288.0  |
