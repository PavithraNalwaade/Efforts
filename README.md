select a.lylt_cust_prfl_id ,sum(a.lylt_lgr_entry_am)
from glbl_lylt_lgr.glbl_lylt_lgr_entry AS a
full join glbl_lylt_lgr.glbl_lylt_lgr_event AS b
on a.lylt_lgr_event_id= b.lylt_lgr_event_id
full join glbl_lylt_lgr.glbl_lylt_lgr_spend_event as c
on c.lylt_lgr_event_id = b.lylt_lgr_event_id
where a.lylt_cust_prfl_id in('e38e9676-f1c9-4af0-8cb3-2735498c05d0')
and cast(a.post_ts as text) <='2023-09-19%'
and a.act_type_cd='REWARD'
group by  a.lylt_cust_prfl_id;
