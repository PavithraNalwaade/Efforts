SELECT 
    a.lylt_cust_prfl_id,
    SUM(a.lylt_lgr_entry_am) AS total_entry_amount
FROM 
    glbl_lylt_lgr.glbl_lylt_lgr_entry AS a
FULL JOIN 
    glbl_lylt_lgr.glbl_lylt_lgr_event AS b 
    ON a.lylt_lgr_event_id = b.lylt_lgr_event_id
FULL JOIN 
    glbl_lylt_lgr.glbl_lylt_lgr_spend_event AS c 
    ON c.lylt_lgr_event_id = b.lylt_lgr_event_id
WHERE 
    a.post_ts <= '2023-09-19'
    AND a.act_type_cd = 'REWARD'
GROUP BY 
    a.lylt_cust_prfl_id;
