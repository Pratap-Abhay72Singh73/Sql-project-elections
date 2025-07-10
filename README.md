# Sql-project-elections
# 1 find out total seats 
select distinct count(Parliament_Constituency) as total_seats from constituencywise_results;
# 2 total no seats available for elections in each state
select s.state as State_name,count(cr.Parliament_Constituency) as total_seats from constituencywise_results cr 
inner join statewise_results sr on cr.Parliament_Constituency=sr.Parliament_Constituency
inner join states s on sr.State_ID=s.State_ID
group by s.state
order by s.state;

# 3 Total Seats Won by NDA Alliance 
SELECT 
    SUM(CASE 
            WHEN party IN (
                'Bharatiya Janata Party - BJP', 
                'Telugu Desam - TDP', 
				'Janata Dal  (United) - JD(U)',
                'Shiv Sena - SHS', 
                'AJSU Party - AJSUP', 
                'Apna Dal (Soneylal) - ADAL', 
                'Asom Gana Parishad - AGP',
                'Hindustani Awam Morcha (Secular) - HAMS', 
                'Janasena Party - JnP', 
				'Janata Dal  (Secular) - JD(S)',
                'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                'Nationalist Congress Party - NCP',
                'Rashtriya Lok Dal - RLD', 
                'Sikkim Krantikari Morcha - SKM'
            ) THEN Won
            ELSE 0 
        END) AS NDA_Total_Seats_Won
FROM 
      partywise_results;
      
      
# 4 seats won by nda alliance parties 
select Party as Party_Name,Won as seats_won
from partywise_results
where party in( 
				'Bharatiya Janata Party - BJP', 
                'Telugu Desam - TDP', 
				'Janata Dal  (United) - JD(U)',
                'Shiv Sena - SHS', 
                'AJSU Party - AJSUP', 
                'Apna Dal (Soneylal) - ADAL', 
                'Asom Gana Parishad - AGP',
                'Hindustani Awam Morcha (Secular) - HAMS', 
                'Janasena Party - JnP', 
				'Janata Dal  (Secular) - JD(S)',
                'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                'Nationalist Congress Party - NCP',
                'Rashtriya Lok Dal - RLD', 
                'Sikkim Krantikari Morcha - SKM'
			)
order by seats_won Desc;

# 5- Seats Won By I.N.D.I.A alliance 
select sum(
            case
                 When party in(
                                 'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
                ) then Won 
                else 0
			end) as seats_won_india 
from partywise_results;

# 6 seats won by I.N.D.I.A alliance parties 
select Party as Party_Name,Won as seats_won
from partywise_results
where party in( 
				'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
			)
order by seats_won Desc;

# 7 - add new column field in table partywise_results to get the Party Allianz as NDA,I.N.D.I.A and Other 
select 
case
    when party in (	
				'Bharatiya Janata Party - BJP', 
                'Telugu Desam - TDP', 
				'Janata Dal  (United) - JD(U)',
                'Shiv Sena - SHS', 
                'AJSU Party - AJSUP', 
                'Apna Dal (Soneylal) - ADAL', 
                'Asom Gana Parishad - AGP',
                'Hindustani Awam Morcha (Secular) - HAMS', 
                'Janasena Party - JnP', 
				'Janata Dal  (Secular) - JD(S)',
                'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                'Nationalist Congress Party - NCP',
                'Rashtriya Lok Dal - RLD', 
                'Sikkim Krantikari Morcha - SKM'
			) then 'NDA'
	when party in (
                'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
                ) then 'I.N.D.I.A'
	ELSE 'OTHER'
end as Party_alliance 
from partywise_results;

# 8-- Winning candidate name there party name ,total vote and the margin of victory for a specific state and constituency ?
select cr.Winning_Candidate,cr.Constituency_Name,cr.Total_Votes,cr.margin,pr.party,s.state
from constituencywise_results cr join statewise_results sr on cr.Parliament_Constituency=sr.Parliament_Constituency
join states s on s.state_ID =sr.state_ID
join partywise_results pr on pr.Party_ID=cr.Party_ID;

# 9-- distibution of evm votes versus postal votes for candidates in a specific Constituency

select cd.EVM_Votes,cd.Postal_Votes,cd.Total_Votes,cd.Candidate,cr.Constituency_Name
from constituencywise_results cr join constituencywise_details cd
on cr.Constituency_ID=cd.Constituency_ID;

# 10-- which parties won the most seats in a state and how many seats did each party win?

select s.state,
case
    when party in (	
				'Bharatiya Janata Party - BJP', 
                'Telugu Desam - TDP', 
				'Janata Dal  (United) - JD(U)',
                'Shiv Sena - SHS', 
                'AJSU Party - AJSUP', 
                'Apna Dal (Soneylal) - ADAL', 
                'Asom Gana Parishad - AGP',
                'Hindustani Awam Morcha (Secular) - HAMS', 
                'Janasena Party - JnP', 
				'Janata Dal  (Secular) - JD(S)',
                'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                'Nationalist Congress Party - NCP',
                'Rashtriya Lok Dal - RLD', 
                'Sikkim Krantikari Morcha - SKM'
			) then 'NDA'
	when party in (
                'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
                ) then 'I.N.D.I.A'
	ELSE 'OTHER'
end as Party_alliance 
from constituencywise_results cr join partywise_results as p 
on cr.Party_ID=p.Party_ID
join statewise_results sr on cr.Parliament_Constituency=sr.Parliament_Constituency
join states s on sr.State_ID=s.State_ID;



#11 -- what is the total number of seat won by each partyalliance (NDA I.N.D.I.A) in each state for the Indian Elections 2024
#above

#12-- which candidate recived the highest number of evm vaotes in each constituency top 10
select  cr.Constituency_Name,cd.Candidate,cd.EVM_Votes
from constituencywise_details cd join constituencywise_results cr 
on cd.Constituency_ID=cr.Constituency_ID
where cd.EVM_Votes=(select max(cd1.EVM_Votes) from constituencywise_details cd1 where cd1.Constituency_ID=cd.Constituency_ID)
order by cd.EVM_Votes desc LIMIT 10 ;

#13--which candidate won and which candidate  was the runner up in each constituency of state for the 2024 election 
with rankedCandidates as(
	select cd.Constituency_ID,cd.Candidate,cd.Party,cd.EVM_Votes,cd.Postal_Votes,cd.EVM_Votes+cd.Postal_Votes as Total_Votes,
    row_number()over(partition by cd.Constituency_ID Order by cd.EVM_Votes +cd.Postal_Votes DESC) as VoteRank
    from constituencywise_details cd join constituencywise_results cr on cd.Constituency_ID=cr.Constituency_ID
    join statewise_results sr on cr.Parliament_Constituency=sr.Parliament_Constituency
    join states s on sr.State_ID=s.State_ID
    where s.State='Himachal Pradesh'
)
select cr.Constituency_Name,max(case when rc.VoteRank=1 then rc.Candidate end ) as Winning_Candidate,
       max(case when rc.VoteRank=2 then rc.Candidate end ) as Runnerup_Candidate
from rankedCandidates rc 
join constituencywise_results cr on rc.Constituency_ID = cr.Constituency_ID
Group by cr.Constituency_Name
order by cr.Constituency_Name;

# 14--For the state of Maharashtra, what are the total number of seats, total number of candidates, total number of parties, total votes (including EVM and postal), and the breakdown of EVM and postal votes?
    
SELECT 
    COUNT(DISTINCT cr.Constituency_ID) AS Total_Seats,
    COUNT(DISTINCT cd.Candidate) AS Total_Candidates,
    COUNT(DISTINCT p.Party) AS Total_Parties,
    SUM(cd.EVM_Votes + cd.Postal_Votes) AS Total_Votes,
    SUM(cd.EVM_Votes) AS Total_EVM_Votes,
    SUM(cd.Postal_Votes) AS Total_Postal_Votes
FROM 
    constituencywise_results cr
JOIN 
    constituencywise_details cd ON cr.Constituency_ID = cd.Constituency_ID
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN 
    states s ON sr.State_ID = s.State_ID
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
WHERE 
    s.State = 'Uttar Pradesh';
