**Hedin - pracovní**


- [ ] TO DO list [https://outlook.office.com/tasks/sharing?InvitationToken=taVozaU9RwHqkgsds32bVQYRYXxEEZzxcekVlG1_W2RyCSjPvy5rQpppzWaOzmVK](https://outlook.office.com/tasks/sharing?InvitationToken=taVozaU9RwHqkgsds32bVQYRYXxEEZzxcekVlG1_W2RyCSjPvy5rQpppzWaOzmVKk)
	- [ ] NIC
	- [ ]

- [ ] EXCEL, ATD.
    
    - EXCEL
        
        - [[ZÁKLADY EXCELU]]
            
        - Xlookup
            
            - [https://www.jiribenedikt.com/materialy/excel/xlookup/](https://www.jiribenedikt.com/materialy/excel/xlookup/)
                
    - POWER QWERY
        
    - POWER BI
        
    - nevim
        
- [ ] SKLADNICI
    
     - [ ] IFTTT
```
> 	Contents from fpdf import FPDF Text content for the PDF text_content = """ Krok za krokem v IFTTT: Vytvoření účtu na IFTTT: Přejděte na [ifttt.com](http://ifttt.com/) a klikněte na Zaregistrovat se. Zaregistrujte se pomocí svého emailu nebo se přihlaste pomocí Google nebo Facebook účtu. Propojení služeb: Po přihlášení klikněte na Prozkoumat v horním menu. Vyhledejte a propojte služby, které chcete použít (např. Gmail a Microsoft To Do). Vytvoření nového appletu: Klikněte na Vytvořit v horním menu. Klikněte na Pokud toto a vyberte službu Gmail. Vyberte spouštěč Nový email v doručené poště od. Zadejte emailovou adresu [skladnici@hedinautomotive.cz](mailto:skladnici@hedinautomotive.cz) a klikněte na Vytvořit spouštěč. Nastavení akce: Klikněte na Pak tamto a vyberte službu Microsoft To Do. Vyberte akci Vytvořit úkol. Nastavte detaily úkolu, jako je název, termín a popis. Můžete například použít předmět a tělo emailu jako název a popis úkolu. Klikněte na Vytvořit akci. Dokončení appletu: Pojmenujte svůj applet (např. "Vytvořit úkol z emailu od skladníků"). Klikněte na Dokončit. Alternativní řešení: Použití existujících spouštěčů a akcí: Můžete zkusit použít obecnější spouštěče, jako je New email in inbox (Nový email v doručené poště) a poté filtrovat emaily podle adresy v akci. Použití Zapier: Zapier nabízí více možností pro automatizaci emailů a úkolů. Můžete vytvořit podobný pracovní postup v Zapieru, který automaticky vytvoří úkol v Microsoft To Do nebo jiné aplikaci, když přijde email od konkrétní adresy. Použití Microsoft Power Automate: Pokud máte přístup k Power Automate, můžete vytvořit tok, který automaticky vytvoří úkol z emailu. I když máte omezená oprávnění, můžete požádat správce o pomoc s nastavením. Jak nastavit obecný spouštěč v IFTTT: Vytvoření nového appletu: Klikněte na Vytvořit v horním menu. Klikněte na Pokud toto a vyberte službu Email. Vyberte spouštěč New email in inbox (Nový email v doručené poště). Nastavení akce: Klikněte na Pak tamto a vyberte službu Microsoft To Do. Vyberte akci Create a task (Vytvořit úkol). Nastavte detaily úkolu, jako je název, termín a popis. Můžete například použít předmět a tělo emailu jako název a popis úkolu. Klikněte na Vytvořit akci. Dokončení appletu: Pojmenujte svůj applet (např. "Vytvořit úkol z emailu"). Klikněte na Dokončit. Tímto způsobem můžete začít automatizovat úkoly, i když váš specifický spouštěč ještě není k dispozici. Pokud budete potřebovat další pomoc nebo máte další otázky, dejte mi vědět! 😊 """ Create instance of FPDF class pdf = FPDF() Add a page pdf.add_page() Set font pdf.set_font("Arial", size = 12) Add text content to PDF for line in text_content.split('\n'): pdf.cell(200, 10, txt = line, ln = True) Save the PDF with name "IFTTTAutomationSteps.pdf" pdf.output("IFTTTAutomationSteps.pdf") print("PDF file 'IFTTTAutomationSteps.pdf' has been created successfully.")
```
        
