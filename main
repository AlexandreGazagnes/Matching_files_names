#!/usr/bin/env python3

###############################################################################
###############################################################################
#       script_matching_noms_fichiers_v1.1.lts
###############################################################################
###############################################################################


# auteur Alexandre GAZAGNES
# date 01/05/2017



###############################################################################
#       IMPORT
###############################################################################


import os



###############################################################################
#       CONSTANTES / VARIABLES
###############################################################################


nom_fichier = "Liste_fichiers.txt"

var_chaine = ""



###############################################################################
#       FONCTIONS
###############################################################################


def menu_principal():

	while True : 
		rep = input("""Voulez-vous créer un fichier de liste de fichiers ou faire une analyse complete?
			Tappez : 
			- 1 / pour créer une liste du nom des fichiers dans un dossier spécifique (choix par défaut = <Entree>)
			- 2 / pour une analyse complete\n""")

		if rep in ["1","2",""]:
			if rep == "" : rep = "1"
			return rep 
		else:
			print("choix incorrect\n")


def menu_search():

	valid = False

	while not valid : 

		rep = input("""\nVoulez-vous:
			1 - Créer automatiquement une liste? par défault tappez <Entree> 
			2 - Importer une chaine (CRTL-C+V)?, 
			3 - Utiliser un fichier de liste déja existant?
			4 - Utliser une variable interne au script 
			Tappez 1,2,3 ou 4 pour valider votre choix\n""")

		if rep in ["", "1","2","3","4"]: 
			if rep == "" : rep = "1"
			valid = True
		else : 
			print("Erreur saisie\n")

	if rep == "1" : 
		repertoire = choix_rep_source()
		input(repertoire)
		liste = sorted(os.listdir(repertoire))
		input(liste)
		chaine = convertir_liste_chaine(liste)
		input(chaine)
	elif rep == "2" :
		chaine = input("Veuillez copier la liste des fichiers à étudier\n\n")
	elif rep == "3" :
		repertoire, chaine = importer_fichier()
	elif rep == "4" :
		repertoire, chaine = os.getcwd(), var_chaine
	else : 
		input("erreur\n")

	return repertoire, chaine.lower()


def choix_rep_source():

	while True : 

		rep = input("\nNous sommes actuellement dans le dossier {},\nvoulez vous garder ce dossier comme dossier principal?\n<Entree> pour 'Oui', autre touche pour 'Non' \n"\
			.format(os.getcwd()))
		
		if not rep :
			return os.getcwd()
		else:
			dossier = input("Veuillez entrer un chemin de dossier : '/home/Fred/Documents...' \n")
			try:
				os.chdir(dossier)
				return dossier
			except:
				print("\nChemin incorrect\n")


def choix_nom_fichier():

	while True : 

		rep = input("le fichier que l'on va créer s'appelle par défault {},\nTappez <Entree> si cela vous convient, ou le nom personnalisé de votre dssier\n"\
			.format(nom_fichier))
		
		if not rep :
			return(nom_fichier)
		else :
			if ".txt" in rep : 
				return rep
			else:
				return str(rep + ".txt")


def convertir_liste_chaine(liste):
	chaine = ""
	for i in liste:
		chaine += str(i) + "\n"
	return chaine.lower()


def enregistrer_chaine(repertoire, nom_fichier, chaine):
	fi = open(nom_fichier, "w")
	fi.write(chaine)
	fi.close()


def importer_fichier():

	valid = False

	while not valid : 

		rep = input("Nous sommes actuellement dans le dossier {}, le fichier est-il dans ce dossier?\n<Entree> pour 'Oui', autre touche pour 'Non' \n"\
			.format(os.getcwd()))
		
		if not rep :
			fichier = input("Veuillez entrer le nom fichier par exemple 'liste.txt' \n")
			if os.path.isfile(os.getcwd() +"/"+ fichier) :
				valid = True
				repertoire = os.getcwd()
			else : 
				input("Fichier incorrect\n")
		else :
			repertoire = choix_rep_source()
			fichier = input("Veuillez entrer le fichier par exemple 'liste.txt' \n")
			if os.path.isfile(repertoire +"/"+ fichier):
				valid = True
			else:
				input("Fichier incorrect\n")

	objet = open(repertoire +"/"+fichier, "r")
	chaine = objet.read()
	objet.close()

	return repertoire, chaine.lower()


def choix_mots_search():
	mot = (input("Veuillez entrer le mot à trouver\nséparer plusieurs mots par une vrigule ','\n\n")).lower()
	liste_mots = mot.split(",")
	return liste_mots


def search_fichiers_liste(liste_mots, chaine): 


	if len(liste_mots) == 1 : 
		return chaine.count(liste_mots[0])

	elif len(liste_mots)>1 :
		elements_presents = list() 

		for mot in liste_mots : 
			if mot in chaine:
				elements_presents.append(chaine.count(mot))
		return elements_presents

	else : 
		input("Erreur\n")



###############################################################################
#       MAIN
###############################################################################


if __name__ == "__main__" : 


	mode = menu_principal()

	if mode == "1" : 

		repertoire = choix_rep_source()
		input("le répertoire choisi est {} \n".format(repertoire))
		nom_fichier = choix_nom_fichier()
		input("le nom du fichier créé est {} \n".format(nom_fichier))
		liste = sorted(os.listdir(repertoire))
		chaine = convertir_liste_chaine(liste)
		input("la liste des fichiers est \n{} \n\net sa chaine relative est \n{}\n\n ".format(liste, chaine))

		enregistrer_chaine(repertoire, nom_fichier, chaine)

	elif mode == "2":

		(repertoire, chaine) = menu_search()

		# boucle principale
		cont =True
		while cont : 

			liste_mots = choix_mots_search()
			resultat = search_fichiers_liste(liste_mots, chaine)
			input("le(s) terme(s) {} est/sont présent(s) (respectivement) {} fois dans notre liste.\n".format(liste_mots, resultat))

			cont = input("Voulez-vous continuer?\n<Entree> pour 'Oui', autre touche pour 'non'\n ")
			if not cont : cont = True
			else : cont = False


		rep = input("Voulez vous enregistrer la liste des noms de fichiers? \n<Entree> pour Oui, autre touche pour Non\n")
		if not rep :
			repertoire = choix_rep_source()
			enregistrer_chaine(repertoire, nom_fichier, chaine)
