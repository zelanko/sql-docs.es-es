---
title: "Especificar cómo se propagan los cambios para los artículos transaccionales | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transactional replication, propagation methods
ms.assetid: a10c5001-22cc-4667-8f0b-3d0818dca2e9
caps.latest.revision: "48"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9cee636f1b2188ddf72d63feeaedc7b955446ea3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="transactional-articles---specify-how-changes-are-propagated"></a>Artículos transaccionales: especificar cómo se propagan los cambios
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La replicación transaccional permite especificar cómo se propagan los cambios de datos del publicador a los suscriptores. Para cada tabla publicada, puede especificar uno de los cuatro métodos siguientes para propagar cada operación (INSERT, UPDATE o DELETE) al suscriptor:  
  
-   Especifique que la replicación transaccional debe crear un script para un procedimiento almacenado y posteriormente, llamarlo para propagar los cambios a los suscriptores (la opción predeterminada).  
  
-   Especifique que el cambio debe propagarse utilizando una instrucción INSERT, UPDATE o DELETE (la opción predeterminada para los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ).  
  
-   Especifique que debe utilizarse un procedimiento almacenado personalizado.  
  
-   Especifique que esta acción no debe realizarse en ningún suscriptor. Las transacciones de este tipo no se replican.  
  
 De forma predeterminada, la replicación transaccional propaga los cambios a los suscriptores a través de una serie de procedimientos almacenados que se instalan en cada suscriptor. Cuando se produce una inserción, una actualización o una eliminación en una tabla del publicador, la operación se convierte en una llamada a un procedimiento almacenado en el suscriptor. El procedimiento almacenado acepta parámetros que se asignan a las columnas de la tabla y permiten cambiar estas columnas en el suscriptor.  
  
 Para establecer el método de propagación para el cambio de datos en artículos transaccionales, vea [Set the Propagation Method for Data Changes to Transactional Articles](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md).  
  
## <a name="default-and-custom-stored-procedures"></a>Procedimientos almacenados predeterminados y personalizados  
 Los tres procedimientos que crea la replicación de forma predeterminada en cada artículo de la tabla son:  
  
-   **sp_MSins_\<** *nombreDeTabla* **>**, que controla las inserciones.  
  
-   **sp_MSupd_\<** *nombreDeTabla* **>**, que controla las actualizaciones.  
  
-   **sp_MSdel_\<** *nombreDeTabla* **>**, que controla las eliminaciones.  
  
 El **\<***nombreDeTabla***>** utilizado en el procedimiento depende de cómo se haya agregado el artículo a la publicación y de si la base de datos de suscripciones contiene una tabla del mismo nombre con un propietario distinto.  
  
 Cualquiera de estos procedimientos se puede sustituir por un procedimiento personalizado que se especifica al agregar un artículo a una publicación. Los procedimientos personalizados se utilizan si una aplicación requiere lógica personalizada, por ejemplo al insertar datos en una tabla de auditoría cuando se actualiza una fila en el suscriptor. Para obtener más información acerca de cómo especificar procedimientos almacenados personalizados, vea los temas de procedimientos indicados anteriormente.  
  
 Si especifica los procedimientos de replicación predeterminados o procedimientos personalizados, también debe especificar la sintaxis de llamada para cada procedimiento (la replicación selecciona los valores predeterminados si utiliza los procedimientos predeterminados). La sintaxis de llamada determina la estructura de los parámetros proporcionados al procedimiento y la cantidad de información que se envía al suscriptor con cada cambio de datos. Para obtener más información, vea la sección "Sintaxis de llamada para procedimientos almacenados" en este tema.  
  
### <a name="considerations-for-using-custom-stored-procedures"></a>Consideraciones para utilizar procedimientos almacenados personalizados  
 Tenga en cuenta los siguientes aspectos cuando utilice procedimientos almacenados personalizados:  
  
-   Debe proporcionar soporte para la lógica personalizada en el procedimiento almacenado; [!INCLUDE[msCoName](../../../includes/msconame-md.md)] no proporciona soporte para la lógica personalizada.  
  
-   Para evitar conflictos con las transacciones utilizadas en la replicación, no se deben utilizar transacciones explícitas en los procedimientos personalizados.  
  
-   Por lo general, el esquema del suscriptor es idéntico al del publicador, pero también puede ser un subconjunto del esquema del publicador, si se utiliza el filtrado de columnas. No obstante, si necesita transformar el esquema al mover los datos para que el esquema del suscriptor no sea un subconjunto del esquema del publicador, la solución recomendada es [!INCLUDE[ssISCurrent](../../../includes/ssiscurrent-md.md)] . Para más información, vea [SQL Server Integration Services](../../../integration-services/sql-server-integration-services.md).  
  
-   Si realiza cambios de esquema en una tabla publicada, deberá volver a generar los procedimientos personalizados. Para más información, vea [Volver a generar procedimientos transaccionales personalizados para reflejar cambios de esquema](../../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
-   Si usa un valor mayor que 1 para el parámetro **-SubscriptionStreams** del Agente de distribución, debe asegurarse de que las actualizaciones de las columnas de clave principal se lleven a cabo correctamente. Por ejemplo:  
  
    ```  
    update ... set pk = 2 where pk = 1 -- update 1  
    update ... set pk = 3 where pk = 2 -- update 2  
    ```  
  
     Si el Agente de distribución utiliza más de una conexión, estas dos actualizaciones podrían replicarse a través de conexiones distintas. Si se aplica primero la actualización 1, no hay problema, pero si se aplica primero la actualización 2, el resultado será '0 filas afectadas', ya que aún no ha tenido lugar la actualización 1. Los procedimientos predeterminados controlan esta situación generando un error si no hay ninguna fila afectada en una actualización:  
  
    ```  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sys.sp_MSreplraiserror 20598  
    ```  
  
     La generación del error obliga al Agente de distribución a volver a intentar la actualización a través de una sola conexión, lo cual se llevará a cabo correctamente. Los procedimientos almacenados personalizados deben incluir una lógica similar.  
  
### <a name="call-syntax-for-stored-procedures"></a>Sintaxis de llamada para procedimientos almacenados  
 Hay cinco opciones para la sintaxis que se utiliza para llamar a los procedimientos empleados en la replicación transaccional:  
  
-   Sintaxis CALL Se puede utilizar para inserciones, actualizaciones y eliminaciones. De forma predeterminada, la replicación utiliza esta sintaxis para las inserciones y las eliminaciones.  
  
-   Sintaxis SCALL. Solo se puede utilizar para las actualizaciones. De forma predeterminada, la replicación utiliza esta sintaxis para las actualizaciones.  
  
-   Sintaxis MCALL Solo se puede utilizar para las actualizaciones.  
  
-   Sintaxis XCALL Se puede utilizar para actualizaciones y eliminaciones.  
  
-   VCALL. Se utiliza para las suscripciones actualizables. Exclusivamente para uso interno.  
  
 Cada método difiere en la cantidad de datos propagados al suscriptor. Por ejemplo, SCALL solo pasa valores para las columnas que resultan afectadas por una actualización. En cambio, XCALL utiliza todas las columnas (hayan sido afectadas o no por la actualización) y todos los valores de datos antiguos para cada columna. En muchos casos, SCALL es apropiado para las actualizaciones, pero si su aplicación necesita todos los valores de datos durante una actualización, XCALL permite utilizarlos.  
  
#### <a name="call-syntax"></a>Sintaxis CALL  
 Procedimientos almacenados INSERT  
 Los procedimientos almacenados que controlan instrucciones INSERT recibirán los valores insertados de todas las columnas:  
  
```  
c1, c2, c3,... cn  
```  
  
 Procedimientos almacenados UPDATE  
 Los procedimientos almacenados que controlan instrucciones UPDATE recibirán los valores actualizados de todas las columnas definidas en el artículo, seguidas de los valores originales de las columnas de clave principal (no se intenta determinar qué columnas se modificaron):  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn  
```  
  
 Procedimientos almacenados DELETE  
 Los procedimientos almacenados que controlan instrucciones DELETE recibirán valores de las columnas de clave principal:  
  
```  
pkc1, pkc2, pkc3,... pkcn  
```  
  
#### <a name="scall-syntax"></a>Sintaxis SCALL  
 Procedimientos almacenados UPDATE  
 Los procedimientos almacenados que controlan instrucciones UPDATE solo recibirán los valores actualizados de las columnas que hayan cambiado, seguidos de los valores originales de las columnas de clave principal y de un parámetro de máscara de bits (**binary(n)**) que indica las columnas que han cambiado: En el siguiente ejemplo, la columna 2 (c2) no ha cambiado:  
  
```  
c1, , c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="mcall-syntax"></a>Sintaxis MCALL  
 Procedimientos almacenados UPDATE  
 Los procedimientos almacenados que controlan instrucciones UPDATE recibirán los valores actualizados de todas las columnas definidas en el artículo, seguidos de los valores originales de las columnas de clave principal y de un parámetro de máscara de bits (**binary(n)**) que indica las columnas que han cambiado:  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="xcall-syntax"></a>Sintaxis XCALL  
 Procedimientos almacenados UPDATE  
 Los procedimientos almacenados que controlan instrucciones UPDATE recibirán los valores originales (es decir, la imagen anterior) de todas las columnas definidas en el artículo, seguidos de los valores actualizados (la imagen posterior) de todas las columnas definidas en el artículo.  
  
```  
old-c1, old-c2, old-c3,... old-cn, c1, c2, c3,... cn,  
```  
  
 Procedimientos almacenados DELETE  
 Los procedimientos almacenados que controlan instrucciones UPDATE recibirán los valores originales (es decir, la imagen anterior) de todas las columnas definidas en el artículo.  
  
```  
old-c1, old-c2, old-c3,... old-cn  
```  
  
> [!NOTE]  
>  Al utilizar XCALL, se espera que los valores de imagen anterior de las columnas **text** e **image** sean NULL.  
  
## <a name="examples"></a>Ejemplos  
 A continuación se indican los procedimientos predeterminados creados por la `Vendor Table` en la base de datos de ejemplo de [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] .  
  
```  
--INSERT procedure using CALL syntax  
create procedure [sp_MSins_PurchasingVendor]   
  @c1 int,@c2 nvarchar(15),@c3 nvarchar(50),@c4 tinyint,@c5 bit,@c6 bit,@c7 nvarchar(1024),@c8 datetime  
as   
begin   
insert into [Purchasing].[Vendor]([VendorID]  
,[AccountNumber]  
,[Name]  
,[CreditRating]  
,[PreferredVendorStatus]  
,[ActiveFlag]  
,[PurchasingWebServiceURL]  
,[ModifiedDate])  
values (   
 @c1  
,@c2  
,@c3  
,@c4  
,@c5  
,@c6  
,@c7  
,@c8  
 )   
end  
go  
  
--UPDATE procedure using SCALL syntax  
create procedure [sp_MSupd_PurchasingVendor]   
 @c1 int = null,@c2 nvarchar(15) = null,@c3 nvarchar(50) = null,@c4 tinyint = null,@c5 bit = null,@c6 bit = null,@c7 nvarchar(1024) = null,@c8 datetime = null,@pkc1 int  
,@bitmap binary(2)  
as  
begin  
update [Purchasing].[Vendor] set   
 [AccountNumber] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [AccountNumber] end  
,[Name] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [Name] end  
,[CreditRating] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [CreditRating] end  
,[PreferredVendorStatus] = case substring(@bitmap,1,1) & 16 when 16 then @c5 else [PreferredVendorStatus] end  
,[ActiveFlag] = case substring(@bitmap,1,1) & 32 when 32 then @c6 else [ActiveFlag] end  
,[PurchasingWebServiceURL] = case substring(@bitmap,1,1) & 64 when 64 then @c7 else [PurchasingWebServiceURL] end  
,[ModifiedDate] = case substring(@bitmap,1,1) & 128 when 128 then @c8 else [ModifiedDate] end  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end  
go  
  
--DELETE procedure using CALL syntax  
create procedure [sp_MSdel_PurchasingVendor]   
  @pkc1 int  
as   
begin   
delete [Purchasing].[Vendor]  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end   
go  
```  
  
## <a name="see-also"></a>Vea también  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
