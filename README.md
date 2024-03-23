# Analisis-kinerja-bisnis-Kimia-Farma-
 Mengevaluasi kinerja bisnis Kimia Farma dari tahun 2020 hingga 2023
 ## START CODE HERE ##
 SELECT
  ft.transaction_id,
  ft.date,
  ft.branch_id,
  kc.branch_name,
  kc.kota,
  kc.provinsi,
  kc.rating AS rating_cabang,
  ft.customer_name,
  ft.product_id,
  p.product_name,
  p.price AS actual_price,
  ft.discount_percentage,
  CASE
    WHEN p.price <= 50000 THEN 0.1
    WHEN p.price > 50000 AND p.price <= 100000 THEN 0.15
    WHEN p.price > 100000 AND p.price <= 300000 THEN 0.2
    WHEN p.price > 300000 AND p.price <= 500000 THEN 0.25
    ELSE 0.3
  END AS persentase_gross_laba,
  (p.price - (p.price * ft.discount_percentage)) AS nett_sales,
  ((p.price - (p.price * ft.discount_percentage)) * 
    (CASE
      WHEN p.price <= 50000 THEN 0.1
      WHEN p.price > 50000 AND p.price <= 100000 THEN 0.15
      WHEN p.price > 100000 AND p.price <= 300000 THEN 0.2
      WHEN p.price > 300000 AND p.price <= 500000 THEN 0.25
      ELSE 0.3
    END)) AS nett_profit,
  ft.rating AS rating_transaksi
FROM `kimia-farma-project-418106.Performance_Analytics.kf_final_transaction` AS ft
INNER JOIN `kimia-farma-project-418106.Performance_Analytics.kf_kantor_cabang` AS kc
ON ft.branch_id = kc.branch_id
INNER JOIN `kimia-farma-project-418106.Performance_Analytics.kf_product` AS p
ON ft.product_id = p.product_id;
## END CODE ##


