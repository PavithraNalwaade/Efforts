unknown directive: golang.org/x/textsyntax




pnalwaa@G75FX62577 ptChecks % go get github.com/pkg/errors
go: module github.com/pkg/errors: git ls-remote -q origin in /Users/pnalwaa/go/pkg/mod/cache/vcs/6d82bc6342f8104a35e27089637bd09e9cdb9402f044a75aeb6d5a73e50dad6c: exit status 128:
        fatal: unable to access 'https://github.com/pkg/errors/': Failed to connect to github.com port 443 after 75004 ms: Couldn't connect to server
pnalwaa@G75FX62577 ptChecks % 
















select a.lylt_cust_prfl_id ,sum(a.lylt_lgr_entry_am)
from glbl_lylt_lgr.glbl_lylt_lgr_entry AS a
full join glbl_lylt_lgr.glbl_lylt_lgr_event AS b
on a.lylt_lgr_event_id= b.lylt_lgr_event_id
full join glbl_lylt_lgr.glbl_lylt_lgr_spend_event as c
on c.lylt_lgr_event_id = b.lylt_lgr_event_id
where a.lylt_cust_prfl_id in('a5df7984-61b6-4fc5-9606-35d61964f8c7')
and cast(a.post_ts as text) <= '2024-01-08%'
and a.act_type_cd='REWARD'
group by a.lylt_cust_prfl_id;




--------------





(Select * , tag_prfl_da ->> 'app_approval_date' as prfl_start_date, tag_prfl_da ->> 'status' as Status, tag_prfl_da ->> 'block_code' as REASON, tag_prfl_da ->> 'date_to_cancel' as Cancel_date, ROW_NUMBER()
				OVER(PARTITION BY glbl_lylt_prfl_id 
					 ORDER BY eff_ts DESC) AS res,
				Count(*) over(partition by glbl_lylt_prfl_id) AS cnt
	from glbl_lylt_prfl.glbl_lylt_prfl_dtl
	WHERE glbl_lylt_prfl_id IN (
		select glbl_lylt_prfl_id from glbl_lylt_prfl.glbl_lylt_prfl_dtl
	where tag_nm = 'profile'
	and glbl_lylt_prfl_id in( '2b031b0b-ed58-4c53-bf28-561486ac1f8a'

)
		
	)
and tag_nm = 'instrument' )



ERROR:  relation "glbl_lylt_prfl.glbl_lylt_prfl_dtl" does not exist
LINE 5:  from glbl_lylt_prfl.glbl_lylt_prfl_dtl
              ^ 

SQL state: 42P01
Character: 347















Risk Identified: 
The manual process to fetch and compare product and transaction timestamps took approximately 16–18 hours (2 full working days) for each run. It involved repetitive tasks such as calling APIs, extracting timestamps, and comparing product activity and transaction data. This manual work was time-consuming, prone to human error, and not scalable when dealing with large volumes of data (100,000+ events). As a result, it was difficult to consistently and quickly identify when card transactions were processed on outdated product versions.  

Solution Implemented: 
To address this, I built an automation script using GoLang. The script authenticates and connects to the Event API to retrieve the last posted timestamp for each product. It then fetches related Card Numbers(CMs) and uses those to call the Profile API to get PT (Product Timestamp) effective dates. The script compares and classifies the timestamps into three categories: identical, near-identical, and clearly different. This classification helps in identifying outdated product usage in transaction processing.

Automation Features: 
The script can handle bulk events (100,000 to 1,000,000+), making it scalable and reliable. It is designed to be modular and can be reused with minor changes for other use cases, such as fetching all CMs for a product or extracting payload specific data from bulk broken events.

Before Automation: 
~2 days (16–18 hours) of manual effort per task, supporting only ~10,000 events. Required full-time analyst effort. Accuracy was moderate due to manual validation.

After Automation: 
Now takes ~30 minutes for the same task. Supports 100,000 to over 1,000,000 events. No manual intervention needed. Accuracy is significantly improved due to automated data comparison.

Operational Impact: 
Approximately 96% time saved. 100% of manual work eliminated for this task. Frees up analysts to focus on higher-value work. The script improves speed, accuracy, and scalability. It also supports faster root cause analysis and can be used across multiple usecases.
