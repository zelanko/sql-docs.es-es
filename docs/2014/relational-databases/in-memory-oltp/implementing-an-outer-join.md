---
title: Implementar una combinación externa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 67084043-6b23-4975-b9db-6e49923d4bab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 532cdf5466445f08d5d415799b9f4afab347e77f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192685"
---
# <a name="implementing-an-outer-join"></a>Implementar una combinación externa
  No se admite una combinación externa en los procedimientos almacenados compilados de forma nativa. En el ejemplo siguiente se muestra una forma de implementar la funcionalidad de una combinación externa izquierda en un procedimiento almacenado compilado de forma nativa.  
  
 Los ejemplos usan una variable de tabla para simular un cursor en la parte izquierda de la combinación y una variable de tabla para crear un único conjunto de resultados, que solo es adecuado cuando se procesa un número limitado de filas, ya que ello implica crear una copia adicional de las filas de datos.  
  
 Una variable (@outer) de tipo t1_type se utiliza para recorrer en iteración las filas desde t1, con un tiempo bucle para simular un cursor. La variable @result de tipo t1t2_join_type, a continuación, se utiliza para construir el conjunto de resultados.  
  
 Debe probar el rendimiento de esta solución alternativa para asegurarse de que funciona de la manera esperada en la aplicación.  
  
```  
-- original query:  
select   
   t1.c1 as t1c1,  
   t1.c2 as t1c2,  
   t2.c2 as t2c2,  
   t2.c3 as t2c3  
   from t1 left join t2 on t1.c2=t2.c3  
GO  
  
create table dbo.t1  
(c1 int not null primary key nonclustered,  
c2 int not null) with (memory_optimized=on)  
  
create table dbo.t2  
(c2 int not null primary key nonclustered,  
c3 int not null) with (memory_optimized=on)  
  
INSERT t1 VALUES (1,2)  
INSERT t1 VALUES (2,3)  
INSERT t1 VALUES (3,2)  
INSERT t2 VALUES (2,3)  
INSERT t2 VALUES (4,3)  
GO  
  
create type dbo.t1_type as table  
(  
   id int identity not null primary key nonclustered hash with (bucket_count=1024),  
   c1 int,  
   c2 int  
) with (memory_optimized=on)  
GO  
  
create type dbo.t1t2_join_type as table  
(  
   t1c1 int not null index ix_t1c1,  
   t1c2 int not null,  
   t2c2 int,  
   t2c3 int  
) with (memory_optimized=on)  
GO  
  
-- ====== scenario: generic left join  
  
-- stored procedure including the workaround  
create procedure dbo.usp_left_join  
with native_compilation, execute as owner, schemabinding  
as  
begin atomic with (transaction isolation level = snapshot, language = N'us_english')  
  
   DECLARE @outer dbo.t1_type  
   DECLARE @result dbo.t1t2_join_type  
  
   -- populate the variable used for iterating over the outer rows  
   INSERT @outer(c1, c2) select c1,c2 from dbo.t1  
  
   DECLARE @i int = 1  
   DECLARE @max int = scope_identity()  
  
   DECLARE @t1c1 int  
   DECLARE @t1c2 int  
  
   while @i <= @max  
   begin     
      select @t1c1 = c1, @t1c2 = c2 from @outer where id = @i  
  
      INSERT @result select @t1c1, @t1c2, c2, c3 from dbo.t2 where c3 = @t1c2  
  
      if @@rowcount = 0   
         INSERT @result (t1c1, t1c2) VALUES (@t1c1, @t1c2)  
  
      set @i += 1  
   end  
  
   select   
      t1c1,  
      t1c2,  
      t2c2,  
      t2c3  
   from @result  
end  
GO  
  
exec dbo.usp_left_join  
```  
  
## <a name="see-also"></a>Vea también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
