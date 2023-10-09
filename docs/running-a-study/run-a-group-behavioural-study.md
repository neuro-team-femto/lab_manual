---
description: >-
  This page gives a check-list of what to do to run a group study in the Design
  2 room.
---

# Run a group behavioural study

### For experimenter:

1. Make sure your experiment directory structure is the following:

```
|-- my_experiment
    |-- experiment
	    |-- experiment.py
	    |-- data
    |-- libs
```

2. Log in to the machine with your ens2m.fr id
3. Copy the `my_experiment` folder into `Partage Enseignements/Neuro/`
4.  Run:

    ```sh
    cd path/to/my_experiment
    pip install -t ./libs/ psychopy
    ```
5.  At the top of the experiment script, add the following lines:

    ```python
    import sys
    sys.path.append(../libs) 
    ```
6.  In `my_experiment/experiment/` create a `run.bat` file with the following:

    ```
    @echo off
    python ./experiment.py %*
    ```

### For participant:

1. Log in with ens2m.fr id
2. Copy `my_experiment` folder from `Partage Enseignements/Neuro` to `Desktop/` (takes a few minutes)
3. Run `run.bat`





## Booking the room

* First check the availability of the room on the ENSMM calendar: [https://edt.ens2m.fr/2022-2023/invite](https://edt.ens2m.fr/2022-2023/invite), navigate to "Salles" (rooms), type room number ("0.83.14 (Transfert-Salle Design 2)")
* Then send an email to the ENSMM admin staff so that they book the room for you at your specific timeslots (perhaps give yourself 30min ahead and before for security). Our contact for this is Mrs Charlotte VITALI (charlotte.vitali@ens2m.fr). Mention something along these lines:&#x20;

> _Bonjour Mme Vitali,_ \
> \
> _Je suis XXX et je travaille dans le Département AS2M du laboratoire FEMTO-ST, dans l'équipe de Jean-Julien Aucouturier avec qui vous avez déjà échangé, je crois._ \
> \
> _Nous aurions besoin d'utiliser la salle Design 2 (0.83.14) du bâtiment Transfert pour une expérience pour nos travaux de recherche, et nous aimerions réserver les créneaux suivants:_ \
> \
> _- day/month, from hour to hour_\
> _- day/month, from hour to hour_\
> \
> \
> _Merci beaucoup !_\
> _XXX_
