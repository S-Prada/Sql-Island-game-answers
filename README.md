# Sql-Island-game-answers
https://sql-island.informatik.uni-kl.de/

This is answers to the fun game of sql island

Please Translate the page into english page before trying the game and it makes it simpler to learn sql on it.

This is you!
After the survived plane crash, you will be stuck on SQL Island for the time being. By making progress in the game, you will find a way to escape from this island.

Below are three tables with the information about Village:

VILLAGE (villageid, name, chief)INHABITANT (personid, name, villageid, gender, job, gold, state) ITEM (item, owner)

This field is where you write your commands. The complete game will be controlled by means of the database language SQL.

Lets Start:

Oh dear, what happened? It seems that I am the only survivor of the air crash. Wow, there are some villages on this island.

It seems there are a few people living in these villages. 

1) How can I see a list of all inhabitants?

Answer:) 
Select * from inhabitant;

Query Result:
<img width="1402" height="973" alt="image" src="https://github.com/user-attachments/assets/2c82056b-d32f-4903-85fd-026944811169" />

2) Thank you, Edward! Okay, let's see who is friendly on this island...

select * from inhabitant where state="friendly";

<img width="1260" height="511" alt="image" src="https://github.com/user-attachments/assets/960acbae-ad57-4445-9346-956fd56e75ce" />

3. ) There is no way around getting a sword for myself. I will now try to find a friendly weaponsmith to forge me one. (Hint: You can combine predicates in the WHERE clause with AND)

select * from inhabitant where state="friendly" and job ="weaponsmith";
<img width="1548" height="228" alt="image" src="https://github.com/user-attachments/assets/bf3fd441-ebe6-4c05-8ee3-7f2bdc13b9fc" />

4.) Oh, that does not look good. Maybe other friendly smiths can help you out, e.g. a blacksmith. Try out: job LIKE '%smith' to find all inhabitants whose job ends with 'smith' (% is a wildcard for any number of characters).

select * from inhabitant where state="friendly" and job like "%smith";

<img width="1575" height="441" alt="image" src="https://github.com/user-attachments/assets/b6a8cf12-e8d5-4f32-94df-0e550b88c90e" />

5.) Hi stranger! Where are you going? I'm Paul, I'm the major of Monkeycity. I will go ahead and register you as a citizen. No need to call me stranger! What's my personid? (Hint: Use a SELECT query without an asterisk. In former queries, the * stands for: all columns. Instead of the star, you can also address one or more columns (seperated by a comma) and you will only get the columns you need.)

select personid from inhabitant where name = 'Stranger';

<img width="179" height="149" alt="image" src="https://github.com/user-attachments/assets/8aef2d0f-5472-473b-b1cb-1e3ddb69ef9a" />

6.) Hi Ernest! How much is a sword? I can offer to make you a sword for 150 gold. That's the cheapest you will find! How much gold do you have? 

select gold from inhabitant where personid=20;

<img width="180" height="219" alt="image" src="https://github.com/user-attachments/assets/01645b1c-9863-4ca3-92cc-c1fff7a54881" />


7.) Damn! No mon, no fun. There has to be another option to earn gold other than going to work. Maybe I could collect ownerless items and sell them! Can I make a list of all items that don't belong to anyone? (Hint: You can recognize ownerless items by: WHERE owner IS NULL). So much cool stuff!

select item, owner from item where owner is null;

<img width="396" height="726" alt="image" src="https://github.com/user-attachments/assets/f066f112-250b-44e2-b23b-a75e09e3a714" />

8.) Yay, a coffee cup. Let's collect it! Do you know a trick how to collect all the ownerless items?

update item set owner =20 where owner is null;

Now list all of the items I have!

select * from item where owner =20;

<img width="375" height="729" alt="image" src="https://github.com/user-attachments/assets/8acb17e2-9e88-4cac-8de5-ef83049de024" />

9.) Find a friendly inhabitant who is either a dealer or a merchant. Maybe they want to buy some of my items. (Hint: When you use both AND and OR, don't forget to put brackets correctly!)

select * from inhabitant where state='friendly' and ( job='dealer' or job = 'merchant');

<img width="1500" height="402" alt="image" src="https://github.com/user-attachments/assets/07000209-219d-4e92-974d-35b892dccbcf" />

10.) I'd like to get the ring and the teapot. The rest is nothing but scrap. Please give me the two items. My personid is 15.

update item set owner =15 where (item = 'ring' and owner =20) or(item ='teapot' and owner =20) ;

Thank you!

11.) Here, some gold!

UPDATE inhabitant SET gold = gold + 120 WHERE personid = 20

Unfortunately, that's not enough gold to buy a sword. Seems like I do have to work after all. Maybe it's not a bad idea to change my name from Stranger to my real name before I will apply for a job.

update inhabitant set name = "Prada" where personid= 20;

Since baking is one of my hobbies, why not find a baker who I can work for? (Hint: List all bakers and use 'ORDER BY gold' to sort the results. 'ORDER BY gold DESC' is even better because then the richest baker is on top.)

select * from inhabitant where job="baker" order by gold desc;

<img width="1443" height="417" alt="image" src="https://github.com/user-attachments/assets/bd5fa7fa-ceaf-45f3-8185-c384d8993769" />

Aha, Paul! I know him!

Hi, you again! So, Prada is your name. I saw you want to work as a baker? Okay! You will be paid 1 gold for 100 bread rolls.

(8 hours later...) Here, I made ten thousand bread rolls! I quit! This should be enough money to buy a sword. Let's see what happens with my gold balance.

UPDATE inhabitant SET gold = gold + 100 - 150 WHERE personid = 20

Here's your new sword, Prodo! Now you can go everywhere.

My name is Prada! Thanks anyway!

Is there a pilot on this island by any chance? He could fly me home.

select * from inhabitant where job="pilot";

Oh no, his state is 'kidnapped'.

<img width="1431" height="198" alt="image" src="https://github.com/user-attachments/assets/c2f2e378-5467-46b9-bc58-99d504406191" />

Horrible, the pilot is held captive by Dirty Dieter! I will show you a trick how to find out the name of the village where Dirty Dieter lives.

SELECT village.name FROM village, inhabitant WHERE village.villageid = inhabitant.villageid AND inhabitant.name = 'Dirty Dieter'

<img width="201" height="198" alt="image" src="https://github.com/user-attachments/assets/45b36a53-5596-44df-a680-b5b67f543e91" />

The expression presented here is called a join. It combines the information of the inhabitant table with information of the village table by matching villageid values.

Thanks for the hint! I can use the join to find out the chief's name of the village Onionville. (Hint: In the column 'chief' in the village table, the personid of the chief is stored)

select inhabitant.name from village, inhabitant where village.name = "Onionville" and village.chief = inhabitant.personid;

<img width="198" height="219" alt="image" src="https://github.com/user-attachments/assets/f3389cec-c195-4b72-a408-23215083c980" />

I've got it! I will visit Fred and ask him about Dirty Dieter and the pilot.

Um, how many inhabitants does Onionville have?

SELECT COUNT(*) FROM inhabitant, village WHERE village.villageid = inhabitant.villageid AND village.name = 'Onionville'

<img width="216" height="189" alt="image" src="https://github.com/user-attachments/assets/1074ee25-94f8-4301-aa5c-7ec24bdf4893" />

Hello Prada, the pilot is held captive by Dirty Dieter in his sister's house. Shall I tell you how many women there are in Onionville? Nah, you can figure it out by yourself! (Hint: Women show up as gender = 'f')

select count(*) from inhabitant, village where inhabitant.villageid=village.villageid and village.name="Onionville" and inhabitant.gender='f';

<img width="186" height="195" alt="image" src="https://github.com/user-attachments/assets/29ae9849-8a3a-4071-8972-3590861d49a9" />

Oh, only one woman. What's her name?

select inhabitant.name from inhabitant, village where inhabitant.villageid=village.villageid and village.name="Onionville" and inhabitant.gender='f';

<img width="228" height="201" alt="image" src="https://github.com/user-attachments/assets/5f8bc069-e1f2-49ad-b1ad-69957cde83f5" />

Lets go,

Prada, if you hand me over the entire property of our nearby village Cucumbertown, I will release the pilot. I will show you now what this property consists of.

SELECT SUM(inhabitant.gold) FROM inhabitant, village WHERE village.villageid = inhabitant.villageid AND village.name = 'Cucumbertown'

<img width="489" height="225" alt="image" src="https://github.com/user-attachments/assets/80de60cf-3f27-4e0c-84ff-37a8526bbf04" />

Oh no, baking bread alone can't solve my problems. If I continue working and selling items though, I could earn more gold than the worth of gold inventories of all bakers, dealers and merchants together. How much gold is that?

select sum(inhabitant.gold) from inhabitant, village where inhabitant.villageid=village.villageid and (inhabitant.job in ("baker","dealer","merchant"));

<img width="459" height="204" alt="image" src="https://github.com/user-attachments/assets/97258a2d-dec8-486d-9448-a430a62ff44a" />

That's not enough.

Let's have a look at how much average gold people own, depending on their job.

SELECT job, SUM(inhabitant.gold), AVG(inhabitant.gold) FROM inhabitant GROUP BY job ORDER BY AVG(inhabitant.gold)

<img width="837" height="885" alt="image" src="https://github.com/user-attachments/assets/dbaa21eb-3e20-41b3-8fe7-54193ad41b7f" />

Very interesting: For some reason, butchers own the most gold. How much gold do different inhabitants have on average, depending on their state (friendly, ...)?

select state, avg(gold) from inhabitant group by state;

<img width="582" height="495" alt="image" src="https://github.com/user-attachments/assets/3bdb78b4-570e-4a60-ace8-8243c9d15569" />

Ok, so the only way is to mug the villains.

Or I might as well go ahead and just kill Dirty Dieter with my sword!

DELETE FROM inhabitant WHERE name = 'Dirty Dieter'

Heeeey! Now I'm very angry! What will you do next, Prada?

delete from inhabitant where state = "evil";

Yeah! Now I release the pilot!

update inhabitant set state = "friendly" where state="kidnapped";

Thank's for releasing me, Prada! I will fly you home!

I take my sword, some gold and lots of useless items with me as a souvenir. What a big adventure!

UPDATE inhabitant SET state = 'emigrated' WHERE personid = 20

The game is over. Get your certificate of completion now! If you want to change the name on the certificate, use an UPDATE command on the inhabitants table.

https://sql-island.cs.uni-kl.de/cert.php?id=68a85e9c5c


<img width="2640" height="1650" alt="image" src="https://github.com/user-attachments/assets/0b0ee9b8-162e-4469-9591-77e885c1f781" />

























 




