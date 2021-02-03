1. TEST RIDERS RETURN WHICH HAVE WON MINIMUM TWO CATEGORIES

`TestRider and hasWorldChampionYear min 2 xsd:integer`

2. RETURNS THE DRIVERS WHO WERE RIDERS OF AT LEAST 2 OFFICIAL TEAMS AND 1 SATELLITE TEAM

`isRiderOf min 2 OfficialTeam and isRiderOf min 1 SatelliteTeam`

3. RETURNS CHIEF MECHANIC WHO ARE MECHANICAL LEADERS OF A TEAM WHO HAVE AS A SEASON RIDER
AT LEAST ONE ITALIAN RIDER

`isChiefMechanicOf some (hasSeasonRider only (bornIn value Italy))`

4. LEGENDS THAT DON'T JUST PARTICIPATE IN GRAND PRIX

`Legend and not (participateIn only GranPrix)`

5. RETURN THE TRACK ENGINEERS WHO ARE SATELLITE TEAM ENGINEERS AND THESE TEAMS HAVE
RIDERS THAT DON'T JUST TAKE TESTS

`isTrackOf some (SatelliteTeam and hasRider some (not(participateIn only Test)))`

6. RETURN TO ALL THE DRIVERS WHO ARRIVED FIRST, SECOND AND THIRD IN THE GRAND PRIX OF FRANCE

`Rider and (finishedFirstIn value FrenchGP) and (finishedSecondIn value FrenchGP) and (finishedThirdIn value FrenchGP)`