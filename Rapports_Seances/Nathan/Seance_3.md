Validation et câblage de la partie pneumatique (pompe à vide 12V et électrovanne 12V) pilotée par Arduino via un module relais 2 canaux.

Matériel
Arduino, module relais optocoupleur 2 canaux, pompe 12V, électrovanne 12V, alimentation 12V 3A, connecteurs Wago.

Au cours de cette séance, nous avons validé et câblé la partie pneumatique comprenant une pompe à vide 12V et une électrovanne 12V, pilotées par un Arduino et un module relais optocoupleur 2 canaux. 
Dans un premier temps, les actionneurs ont été testés avec succès en les branchant directement sur l'alimentation 12V 3A. Cependant, lors des premiers essais de pilotage via l'Arduino, 
les actionneurs refusaient de fonctionner malgré l'allumage des LED de contrôle sur le module relais.

Plusieurs problèmes ont été rencontrés et résolus successivement : l'électrovanne a d'abord présenté un léger échauffement sans action, puis nous avons constaté l'absence totale de "clic" mécanique au niveau des relais.
Cela était dû au fait que la partie puissance des bobines (broches JD-VCC) n'était pas alimentée. En raccordant à la fois les broches JD-VCC et VCC au 5V de l'Arduino, les bobines ont enfin reçu le courant nécessaire
pour commuter la puissance 12V provenant des bornes COM vers les sorties NO, tandis que les masses (-) étaient regroupées via un connecteur Wago. Enfin, un programme de test séquentiel a été téléversé sur l'Arduino pour
valider le fonctionnement en boucle des actionneurs.

![Circuit pneumatique Arduino].\image1.jpg

Code de test : 
const int pumpPin = 7;
const int valvePin = 8;

void setup() {
  pinMode(pumpPin, OUTPUT);
  pinMode(valvePin, OUTPUT);
  digitalWrite(pumpPin, HIGH);
  digitalWrite(valvePin, HIGH);
}

void loop() {
  digitalWrite(pumpPin, LOW);  // Pompe ON
  delay(3000);
  digitalWrite(pumpPin, HIGH); // Pompe OFF
  delay(1000);
  digitalWrite(valvePin, LOW); // Électrovanne ON
  delay(3000);
  digitalWrite(valvePin, HIGH);// Électrovanne OFF
  delay(3000);
}

Prochaine Seance : montage et assemblage du robot 
