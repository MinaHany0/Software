
# 03 HVAC Ducts
## Air Terminals Modelling

putting air terminals
- you can use hosted air terminals for referring the ceiling closure

- aligning the air terminals and locking them to the lines needed if possible

- adding the air flow for each air terminal

- notice that the calculated supply air flow doesn't relate to the air terminals, this has relation to the cooling load calculation

- we can install a grill air terminal on duct directly but remember that it can't be a hosted  family

- every duct system can have a distinct name after you finish modelling it
- the duct system name can't be changed unless you mark the entire system

- connected air terminal have a system type and system classification and a definite color
- unconnected air terminal have a system classification but no system type and no color

- notice that the equipment must be a part of your system type when you finish modelling and it will have multiple system types at once as it is connected to many systems

- every family can have multiple types: example: a diffuser family can have 2 types one with 300x300 connector and another with 200x200 connector

- to check if any modification didn't ruin your system, you can use the tab to check if the system is still connected together

- cap open end option will not appear unless you filter our the air terminals from you duct system selection

## Duct Sizing
- remember that you need to make splits before asking revit to size the system as an indication of the 
- remember to remove the sizes that you don't want to be used in automatic sizing from mechanical settings ex : 125mm

- don't forget to create systems for every FCU (supply and return), just select the diffuser and then use option (create system and define it)

## Question :
does every FCU supply and return have a system or all supply and return ducts for all FCU in one zone (for example)
answer: all FCUs supply have the same system type (created by user : Supply FCU) but a system name related to FCU reference number (ex: FCU-G-01)

## <span style="color:rgb(255, 192, 0)">Important</span> : 
disable this option that is new in Revit 24: mechanical setting-> calculations -> enable network based calculations: this was added for the fabrication and will be dealt with later

## System browser:
system browser will show you all created system types and will show all instances created from this system type: 
ex: system type: Supply FCU
ex : created system type instances: FCU-G-01, FCU-G-02, ....

## VAV box

the VAV boxes are treated differently due to its nature: it has 2 sides, one duct from each side and normally the family is configured to have two different duct systems on each side
and the system of this duct will be divided: one before all the VAVs and one after all the VAVs

so you need to do a special configuration: 
- go into the family of the VAV
- link the 2 connectors of the VAV together so Revit will understand that the supply of this side will go into the other side
- make the 2 connectors flow configuration have calculated airflows (no preset)
- and make the system classification : global -> so it will work in any system and it will be correct in the system browser
- if not done in family by default: you need to give the mechanical flow the family parameter "<span style="color:rgb(255, 192, 0)">air flow</span>" -> you can get it by the 2 hyphens next to flow parameter in the properties tab
- in video before this configuration: there were as much systems as number of VAVs, after only one system for all duct system

so that means all the air terminal have preset values
and all VAVs have calculated connector values  and have global system type so it can inherit any system and you need to make the FCU side as in side and the air terminal side as out side (should be done by default I assume)