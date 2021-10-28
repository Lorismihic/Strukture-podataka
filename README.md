# Strukture-podataka

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct _student
{
	char ime[20];
	char prezime[20];
	double bodovi;
}student;

int ProcitajBrojRedakaDatoteke(char* nazivDatoteke);
student* AlocirajISpremiStudente(int brojStudenata, char* nazivDatoteke);
int MaxBrojBodova(student* studenti, int brojStudenata);
int IspisStudenata(student* studenti, int brojStudenata);

int main()
{
	char nazivDatoteke[50] = { 0 };
	int brojRedaka = 0;
	student* studenti = NULL;


	printf("Unesi naziv datoteke:\n");
	scanf(" %s", nazivDatoteke);
	brojRedaka = ProcitajBrojRedakaDatoteke(nazivDatoteke);
	if(brojRedaka > 0)
		printf("Broj redaka je: %d", brojRedaka);
	studenti = AlocirajISpremiStudente(brojRedaka, nazivDatoteke);
	IspisStudenata(studenti, brojRedaka);
	return 0;
}
int ProcitajBrojRedakaDatoteke(char* nazivDatoteke)
{
	FILE* datoteka = NULL;
	int brojRedaka = 0;
	char naziv[1024];

	datoteka = fopen(nazivDatoteke, "r");
	if (!datoteka)
	{
		printf("Nije se otvorilo!\n");
		return -1;
	}
	while (!feof(datoteka))
	{
		fgets(naziv, sizeof(naziv), datoteka);
		brojRedaka++;
	}
	fclose(datoteka);
	return brojRedaka;
}
student* AlocirajISpremiStudente(int brojStudenata, char* nazivDatoteke)
{
	FILE* datoteka = NULL;
	student* studenti = NULL;
	int brojRedaka = 0;

	studenti = (student*)malloc(brojStudenata * sizeof(student));
	if (!studenti)
	{
		printf("Neuspjesna alokacija memorije!\n");
		return NULL;

	}

	datoteka = fopen(nazivDatoteke, "r");
	if (!datoteka)
	{
		printf("Nije se otvorilo!\n");
		return NULL;
	}
	while (!feof(datoteka))
	{
		fscanf(datoteka, " %s %s %lf", studenti[brojRedaka].ime,
			studenti[brojRedaka].prezime,
			&studenti[brojRedaka].bodovi);
			brojRedaka++;
	}
	fclose(datoteka);
	return studenti;
}

int MaxBrojBodova(student* studenti, int brojStudenata){
	int i = 0;
	int max=0;
	for (i; i < brojStudenata; i++)
	{
		if (studenti[i].bodovi>max){
			max=studenti[i].bodovi;
		}

	}
	return max;
}

int IspisStudenata(student* studenti, int brojStudenata)
{
	int i = 0;
	for (i; i < brojStudenata; i++)
	{
		printf("Ime: %s\t Prezime: %s\t Bodovi: %lf%lf\t\n", studenti[i].ime, studenti[i].prezime, studenti[i].bodovi, studenti[i].bodovi/MaxBrojBodova(student* studenti,brojStudenata)*100);
	}
	return 0;
}
