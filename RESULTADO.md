# Listar todos Clientes que não tenham realizado uma compra;

```SQL
  select * 
  from 
    sales.customers A
  where not exists (
    select * 
    from 
      sales.orders B
    where 
      B.customer_id = A.customer_id
    )
  ;
```

# Listar os Produtos que não tenham sido comprados

```SQL
  select * 
  from 
  	production.products A
  where
  	not exists (
  		select *
  		from 
  			sales.order_items B
  		where
  			B.product_id = A.product_id
  	)
  ;
```

# Listar os Produtos sem Estoque

```SQL
  select * 
  from 
  	production.products A join production.stocks B
  		on B.product_id = A.product_id
  where
  	B.quantity = 0
  ;
```

# Agrupar a quantidade de vendas que uma determinada Marca por Loja

```SQL
  select C.store_name, E.brand_name, sum(B.quantity) as qtd_sales
  from 
  	sales.orders A join sales.order_items B
  		on B.order_id = A.order_id
  	join sales.stores C
  		on C.store_id = A.store_id
  	join production.products D
  		on D.product_id = B.product_id
  	join production.brands E
  		on E.brand_id = D.brand_id
  group by
  	C.store_name, E.brand_name
  order by
  	C.store_name, E.brand_name
  ;
```

# Listar os Funcionarios que não estejam relacionados a um Pedido

```SQL
  select * 
  from 
  	sales.staffs A
  where
  	not exists (
  		select * 
  		from 
  			sales.orders B
  		where
  			B.staff_id = A.staff_id
  	)
  ;
```

