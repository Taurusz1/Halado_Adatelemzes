# Titanic Survival Prediction with Machine Learning

## Overview

Ez a dokumentum négy különböző tanulmányból gyűjtött adatokat foglalja össze, amelyek a Titanic utasainak túlélését vizsgálják különböző gépi tanulási modellekkel, például a logisztikus regresszióval (LR), döntési fákkal (DT) és véletlen erdőkkel (RF).

---

## 1. cikk: Survival Prediction and Comparison of the Titanic based on Machine Learning Classifiers

- **Logisztikus regresszió (LR)**:
    - Keresztvalidációs pontszám: **79%**
    - Precision: **88.2%**
    - Recall: **82.9%**
    - AUROC: **0.81**
- **Döntési fák (DT)**:
    - Mélység: **45 és 75**
    - Keresztvalidációs pontszám: **77%**
    - Precision: **86.8%**
    - Recall: **84.6%**
- **Véletlen erdők (RF)**:
    - Mélység: **45 és 75**
    - Pontszám: **79.8%**
    - Precision: **91.9%**
    - Recall: **87.2%**
- **Jellemzők**:
    - **Kor**: mediánnal kitöltve
    - **Kabinszám**: 'Unknown'-ra cserélve
    - **Viteldíj (Fare)**: az osztály szerinti medián értékkel kitöltve
    - **One-hot encoding** alkalmazva a kategóriákra
    - Felesleges oszlopok: PassengerID, Name, Ticket — eltávolítva
    - **Új jellemzők**:
        - **Age * Class**
        - **Fare per Person**
        - **IsAlone** (Family_Size = 1)

---

## 2. cikk: Basic Feature Engineering with the Titanic Data

- **Név oszlop megőrzése**: nem törölték, hanem a címeket (Mr, Mrs, Miss, Master) használták új kategóriaként
- **Kabinszám**:
    - Csak az 1. osztályú utasoknak volt kabinja, a többieknél 'Unknown'
    - Új jellemző: **Deck** — a kabinszámból kinyerve
- **Család mérete (Family Size)**:
    - **SibSp + Parch + 1**
- **Új jellemzők**:
    - **Age * Class**: `df['Age'] * df['Pclass']`
    - **Fare per Person**: `df['Fare'] / (df['Family_Size'] + 1)`

---

## 3. cikk: Predicting the Likelihood of Survival of Titanic’s Passengers by Machine Learning

- **Megfigyelések**:
    - Kevés gyermek utazott dadával, ezért **Parch = 0**
    - A túlélés valószínűsége magasabb **18 és 30 év közötti férfiaknál** és **14 és 40 év közötti nőknél**
    - **5-18 éves férfiaknál** alacsonyabb túlélési arány
    - **Osztály (Pclass)** kiemelten fontos: 1. osztályon a legmagasabb a túlélési arány
- **Modellek teljesítménye**:
    - Döntési fa: **99.29%** pontosság (tréning adatokon)
    - Logisztikus regresszió: **81.11%** pontosság (teszt adatokon)
    - Random Forest: **97.53%** (tréning adatokon), **80.41%** (teszt adatokon)

---

## 4. cikk: Analyzing Titanic Disaster using Machine Learning Algorithms

- **Címek és kor kapcsolatának vizsgálata**:
    - A **Miss** általában fiatalabb, mint a **Mrs**
    - Hiányzó életkort a címek medián korával pótolták (pl. Mrs. című nők medián korával)
- **Hiányzó értékek pótlása**:
    - Életkor (Age): címek medián életkorával
    - Kabin (Cabin): 'Unknown'
- **Jellemzők**:
    - Életkor (Age)
    - Nem (Sex)
    - Cím (Title)
    - Kabinszám (Cabin)
    - Osztály (Pclass)
    - Beszállás helye (Embarked)
    - Viteldíj (Fare)
    - Család mérete (Family Size, SibSp + Parch)

---

## Következtetés

A négy cikkből származó megközelítések közös pontokat mutatnak a Titanic túlélés előrejelzésének modellezésében. A **Random Forest** modellek következetesen jobban teljesítettek, míg a **logisztikus regresszió** a pénzügyi modellezésben bevált egyszerűsége miatt továbbra is alapmodell marad. Az új jellemzők bevezetése — különösen a **címek, családméret és osztály kombinációk** — jelentősen hozzájárult a modellek pontosságához.
