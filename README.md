# Lab-1
Киберспортсмены
esport_player(s1, 'Niko', 'FaZe Clan', 27).
esport_player(s2, 'S1mple', 'Natus Vincere', 26).
esport_player(s3, 'ZywOo', 'Team Vitality', 23).
esport_player(s4, 'dev1ce', 'Ninjas in Pyjamas', 27).
esport_player(s5, 'coldzera', 'Loud', 29).
esport_player(s6, 'shroud', 'Cloud9', 30).
esport_player(s7, 'kennyS', 'G2 Esports', 27).
esport_player(s8, 'GeT_RiGhT', 'Ninjas in Pyjamas', 34).
esport_player(s9, 'flusha', 'Fnatic', 27).
esport_player(s10, 'rain', 'FaZe Clan', 28).
esport_player(s11, 'B1t', 'Natus Vincere', 20).
esport_player(s12, 'Ethan', 'Evil Geniuses', 24).
esport_player(s13, 'device', 'Astralis', 26).
esport_player(s14, 'apEX', 'Team Vitality', 30).
esport_player(s15, 'NBK-', 'OG', 27).
esport_player(s16, 'ALEX', 'Team Vitality', 25).

Навыки
skill(s1, aim).
skill(s1, strategy).
skill(s2, aim).
skill(s2, clutch).
skill(s3, aim).
skill(s3, support).
skill(s4, strategy).
skill(s4, teamwork).
skill(s5, aim).
skill(s5, leadership).
skill(s6, aim).
skill(s6, teamwork).
skill(s7, aim).
skill(s7, strategy).
skill(s8, experience).
skill(s8, support).
skill(s9, aim).
skill(s9, clutch).
skill(s10, aim).
skill(s10, teamwork).
skill(s11, aim).
skill(s11, support).
skill(s12, strategy).
skill(s12, teamwork).
skill(s13, strategy).
skill(s13, aim).
skill(s14, strategy).
skill(s14, clutch).
skill(s15, leadership).
skill(s15, strategy).
skill(s16, support).
skill(s16, teamwork).

Турниры
tournament(t1, 'IEM Katowice 2020').
tournament(t2, 'ESL One Cologne 2021').
tournament(t3, 'BLAST Premier 2021').
tournament(t4, 'Major Championship 2022').
tournament(t5, 'DreamHack Masters 2019').
tournament(t6, 'ESL Pro League Season 10').
tournament(t7, 'IEM Global Challenge 2020').
tournament(t8, 'BLAST Premier Spring 2021').

Участие в турнирах
participation(s1, t1).
participation(s2, t1).
participation(s3, t2).
participation(s4, t3).
participation(s5, t4).
participation(s6, t5).
participation(s7, t6).
participation(s8, t1).
participation(s9, t2).
participation(s10, t3).
participation(s11, t4).
participation(s12, t5).
participation(s13, t6).
participation(s14, t7).
participation(s15, t8).
participation(s16, t5).

Победы
win(s1, t1).
win(s2, t1).
win(s3, t2).
win(s4, t3).
win(s5, t4).
win(s6, t5).
win(s7, t6).
win(s9, t2).
win(s10, t3).
win(s11, t4).
win(s12, t5).
win(s13, t6).
win(s14, t7).
win(s15, t8).

Правила:

1. Игрок выиграл в турнире
player_won_in_tournament(Player, Tournament) :-
    esport_player(PlayerID, Player, _, _),
    participation(PlayerID, Tournament),
    win(PlayerID, Tournament).

2. Все навыки игрока
player_skills(Player, Skills) :-
    esport_player(PlayerID, Player, _, _),
    findall(Skill, skill(PlayerID, Skill), Skills).

3. Игроки одной команды
players_in_team(Team, Players) :-
    findall(Player, esport_player(ID, Player, Team, _), Players).

4. Игроки с определенным навыком
players_with_skill(Skill, Players) :-
    findall(Player, (esport_player(ID, Player, _, _), skill(ID, Skill)), Players).

5. Количество турниров, в которых участвовал игрок
player_tournaments_count(Player, Count) :-
    esport_player(PlayerID, Player, _, _),
    findall(Tournament, participation(PlayerID, Tournament), Tournaments),
    length(Tournaments, Count).

6. Самый возрастной игрок
oldest_player(Name, Age) :-
    esport_player(ID, Name, _, Age),
    \+ (esport_player(_, _, _, Age2), Age2 > Age).

Запросы:
player_won_in_tournament('S1mple', 'IEM Katowice 2020').
player_skills('Niko', Skills).
players_in_team('FaZe Clan', Players).
players_with_skill(aim, Players).
player_tournaments_count('S1mple', Count).
oldest_player(Name, Age).
