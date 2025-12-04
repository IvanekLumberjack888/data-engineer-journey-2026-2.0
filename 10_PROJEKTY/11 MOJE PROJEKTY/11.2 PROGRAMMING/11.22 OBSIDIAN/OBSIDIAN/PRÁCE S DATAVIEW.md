
## **1. Co je Dataview?**

- **Dataview** umožňuje zobrazit tvoje poznámky jako seznamy, tabulky nebo kalendáře na základě obsahu poznámek.
- Funguje na základě jednoduchého dotazovacího jazyka, podobného SQL.

Například:

- Zobrazíš všechny poznámky s určitým tagem (#tag).
- Najdeš úkoly, které jsi ještě nedokončil.
- Seřadíš projekty podle dat.

---

## **2. Aktivace a kontrola nastavení**

1. **Ověř, že máš Dataview zapnutý:**
    
    - Jdi do `Settings > Community plugins > Dataview` a ujisti se, že je aktivní.
2. **Zapni režim inline dotazů (pokud ještě není):**
    
    - Jdi do `Settings > Dataview` a zaškrtni možnost **Enable inline queries**.

---

## **3. Jednoduché příklady použití**

```dataview
task
```

### **a) Zobrazení úkolů**

- V jakékoliv poznámce napiš:
    
    ````
    ```dataview
    task
    ```
    ````
    
    - To ti ukáže seznam všech úkolů (poznámek, kde máš checkboxy `- [ ]`).
    
---

### **b) Filtr úkolů podle složky**

- Pokud chceš vidět jen úkoly z konkrétní složky, například "PROJEKTY":
    
    ````
    ```dataview
    task from "11_PROJEKTY"
    ```
    ````
    

---

### **c) Vytvoření tabulky**

- Chceš zobrazit tabulku poznámek seřazenou podle názvu:
    
    ````
    ```dataview
    table file.name, file.cday
    from "11_PROJEKTY"
    sort file.name asc
    ```
    ````
    
    - **file.name** = název souboru.
    - **file.cday** = datum vytvoření souboru.
    - **sort** = řazení vzestupně (asc) nebo sestupně (desc).

---

### **d) Zobrazení tagů**

- Pokud chceš vypsat všechny poznámky s tagem #TODO:
    
    ````
    ```dataview
    list from #TODO
    ```
    ````
    

---

## **4. Vytvoření dashboardu**

Můžeš si vytvořit "hlavní přehledovou poznámku" (dashboard), kde budeš mít vše důležité. Například:

````
# 🗂️ Dashboard
## 📋 Úkoly
```dataview
task from "11_PROJEKTY"
```

## 🗓️ Projekty (tabulka)
```dataview
table file.name, file.cday
from "11_PROJEKTY"
sort file.cday desc
```
````

# 🗂️ Dashboard
## 📋 #Úkoly
```dataview
task from "11_PROJEKTY"
```

## 🗓️ #projekty_📂 (tabulka)
```dataview
table file.name, file.cday
from "11_PROJEKTY"
sort file.cday desc
```

---

## **5. Tipy pro práci s Dataview**

- **Přizpůsob si dotazy podle potřeb:** Můžeš kombinovat podmínky, např. úkoly z určité složky, které obsahují konkrétní slova.
- **Zkoušej malé kroky:** Začni jednoduchými dotazy a postupně je rozšiřuj.
- **Dokumentace Dataview:** Pokud chceš jít do hloubky, podívej se do [oficiální dokumentace Dataview](https://blacksmithgu.github.io/obsidian-dataview/).

---

Dej vědět, které z těchto příkladů bys chtěl vyzkoušet jako první, nebo jestli chceš pomoci vytvořit konkrétní dotaz pro tvé poznámky! 😊

