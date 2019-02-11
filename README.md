# EDM5240-devoir2
devoir2 de JB - Quelques cheveux en moins, des cernes mais tout de même un peu content.


# coding utf-8

import json
import csv
import requests

fichier = "banq_rep.csv"

url = "http://collections.banq.qc.ca/api/service-notice?handle=52327/"

entete = {
	"User-Agent":"Jean-Baptiste Demouy - 514/553-9575",
	"From":"jibdemouy@gmail.com"
}

for nb in range(1000,2001):
	urlall = url + str(nb)
	# print(urlall)

	req = requests.get(urlall,headers=entete)
	# print(req)
	if req.status_code == 200:
		alldata = req.json()
		# print(alldata)
		# print("°"*80)

		if alldata["type"]== "audio":			
			s = []
			s.append(alldata["titre"]) # ici, il faudrait ajouter .split("/")) afin de ne prendre en compte que le titre et non les informations suivantes -> Impossible à tester en fin de soirée : Response 500
			s.append(alldata["createurs"][0])
			s.append(alldata["dateCreation"])
			s.append(alldata["descriptionMat"])
			s.append(alldata["url"])
			print(alldata["titre"])
			print(alldata["createurs"][0])
			print(alldata["dateCreation"])
			print(alldata["descriptionMat"])
			print(alldata["url"])
			print("°"*80)

		f2 = open(fichier,"a")
		pouet = csv.writer(f2)
		pouet.writerow(s)


# Problème de serveur "response 500" en fin de soirée. Impossible de tester une dernière fois.
