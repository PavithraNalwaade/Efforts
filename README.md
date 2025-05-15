SELECT 
    a.lylt_cust_prfl_id,
    a.lylt_lgr_entry_am,
    a.post_ts,
    c.roc_spend_am,
    c.trans_id,
    a.act_type_cd
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
    AND a.act_type_cd = 'REWARD';



--------

SELECT 
    a.lylt_cust_prfl_id,
    SUM(a.lylt_lgr_entry_am) AS total_entry_amount,
    MIN(a.post_ts) AS first_post_ts,
    SUM(c.roc_spend_am) AS total_spend_am,
    MIN(c.trans_id) AS sample_trans_id,
    MIN(a.act_type_cd) AS sample_act_type_cd
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
