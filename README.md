# Oving-9
class Quiz: #grunnmur
    
    def __init__(self, spørsmål, alternativ, svar = 0): #init = hovedbrikker (spørsmål, alternativ, svar)
        self.spørsmål = spørsmål
        self.alternativ = alternativ
        self.svar = svar #ikke starte på 0
        
    def __str__(self): #skrive ut class
        utskrift = self.spørsmål + "\n" 
        for index, verdi in enumerate(self.alternativ): #index, verdi i en liste
            utskrift += f"{index + 1}) {verdi}\n" #alternativene (index + verdi)
        return utskrift # gi utskrift
    
    def sjekk_svar(self, riktig_svar):
        if riktig_svar - 1 == self.svar:
            return True
        else: 
            return False
        
    def korrekt_svar_tekst(self):
        korrekt_svar = self.alternativ[self.svar]
        return korrekt_svar
    

spiller_1_poeng = []
spiller_2_poeng = []
    

def start_spill():
    with open ("sporsmaalsfil.txt", "r", encoding="UTF8") as fil:
        for linje in fil:
            linje = linje.split(":")
            alternativ = linje[2].replace("[", " ").replace("]", " ")   
            quiz_spørsmål = Quiz(linje[0],alternativ.split(","),int(linje[1]))
            print(quiz_spørsmål)
            
            spiller_1_svar = int(input("Skriv inn svaret til spiller 1: "))
            spiller_2_svar = int(input("Skriv inn svaret til spiller 2: "))
            
            if quiz_spørsmål.sjekk_svar(spiller_1_svar):
                print("\nSpiller 1: Korrekt")
                spiller_1_poeng.append(1)
            else:
                print("\nSpiller 1: Feil")
            
            if quiz_spørsmål.sjekk_svar(spiller_2_svar):
                print("Spiller 2: Korrekt")
                spiller_2_poeng.append(1)
                print(f"\nKorrekt svar: {quiz_spørsmål.korrekt_svar_tekst()}\n")
            else:
                print("Spiller 2: Feil")
                print(f"\nKorrekt svar: {quiz_spørsmål.korrekt_svar_tekst()}\n")
                
            input("Trykk enter for å fortsette\n")
            
              
start_spill()
print("Resultat:\n\nSpiller 1: ", len(spiller_1_poeng), " Poeng")
print("Spiller 2: ", len((spiller_2_poeng)), " Poeng")
