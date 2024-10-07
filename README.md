## Uitleg queries: bepaling ligduur met en zonder beademing.
Doel: aantal liguren/beddagen uitzetten van patienten die wel vs. niet beademd worden op `ICK1234`. <br>
<b>Voorwaarden:</b> 

1. Bedademd = Tube
2. Indien deels beademd, hele opname meetellen
3. Liever geen post chirurgisch patienten (CTC/KCA) 
4. Alleen opnames gebruiken in de rekensom vab locatie `SK3D` - `SK3G`
5. Voor nu alleen patienten opgenomen in 2023 meegenomen als schatting van ligduur/beddagen. 


<b>Vier queries gebruiken:</b> 

1. Alle opnames `ICK1234` om totale ligduur te berekenen. 
2. Van alle opnames `ICK1234` ligduur berekenen van opnames waarin:
    1. Patiënt geïntubeerd is
    2. Patiënt geëxtubeerd is 
    3. Patiënt gedurende de gehele opname een tube in situ had. 
3. Alle opnames op `ICK1234` waarvan een deelopname een chirurgische ingreep is, welke uitgevoerd is door `CTC` of `KCA`. 
4. Van alle opnames `ICK1234` waarvan een deelopname een chirurgische ingreep is ligduur berekenen van opnames waarin:
    1. Patiënt geïntubeerd is
    2. Patiënt geëxtubeerd is 
    3. Patiënt gedurende de gehele opname een tube in situ had. 

De voorwaarde 'geen tube' is bijna onmogelijk om direct te creëren, daarom zijn er meerdere queries gebruikt om het te berekenen. Bij niet post-cardiothoracale chirurgie kreeg ik geen resultaten terug waarvoor ik nog steeds de oplossing niet gevonden heb. 
De rekensommen aan de hand van hierboven benoemde queries (om te voldoen aan `voorwaarde 3`): 
> `Answer A`: Beddagen/ligduur van niet cardio patiënten met tube: totale duur van `query(2)-query(4)` <br>
> `Answer B`: Beddagen/ligduur van niet cardio patiënten zonder tube: totale duur van `query(1)-query(2)-query(3)`. 
<table>
<tr>
<th> Queries </th>
<th> Gewenste uitslag </th>
</tr>
<tr>
<td>


|query 1     |  cardio   | niet-cardio|          
|---|----|----|        
tube        |     x     |     x                 
niet-tube   |     x     |     x   


</td>
<td>

Answer A    |  cardio   | niet-cardio
|-----|----|----|
tube        |           |     x
niet-tube   |           |     


</td>
</tr>
<tr>
<td>

query 2|cardio|niet-cardio     
|---|----|----|       
|tube|x|x|                 
|niet-tube| |  |

</td>
<td>

Answer B    |  cardio   | niet-cardio
|---|----|----| 
tube        |           |     
niet-tube   |           |     x

</td>
</tr>
<td>

query 3     |  cardio   | niet-cardio
|---|----|----| 
tube        |     x     |      
niet-tube   |     x     |      

</td>
    <td></td>
</tr>

<td>

query 4     |  cardio   | niet-cardio
|---|----|----| 
tube        |     x     |     
niet-tube   |           |     

</td>
<td></td>
</tr>
</table>
    
>`Answer A` (ligduur tube)= query(2) - query(4) <br>
>`Answer B` (ligduur niet-tube )= query(1) - query(2) - query(3)


#### Parameters `Answer A`
Runtime = 00:34:52

