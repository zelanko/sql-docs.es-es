---
title: Configuración de conectividad de PolyBase (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
ms.assetid: 82252e4f-b1d0-49e5-aa0b-3624aade2add
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d86483245f8a4f06dfcb357d5d105539dd56f3a7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67997913"
---
# <a name="polybase-connectivity-configuration-transact-sql"></a>Configuración de conectividad de PolyBase (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  Muestra o cambia la configuración global de PolyBase Hadoop y la conectividad de almacenamiento de blobs de Azure.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
--List all of the configuration options  
sp_configure  
[;]  
  
--Configure Hadoop connectivity  
sp_configure [ @configname = ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@configname=** ] **'** _nombre\_opción_ **'**  
 Es el nombre de una opción de configuración. *option_name* es **varchar(35)** y su valor predeterminado es NULL. Si no se especifica, se devuelve la lista completa de opciones.  
  
 [ **@configvalue=** ] **'** _valor_ **'**  
 Es la nueva configuración. *value* es de tipo **int**y su valor predeterminado es NULL. El valor máximo depende de la opción individual.  
  
 **'conectividad de hadoop'**  
 Especifica el tipo de origen de datos de Hadoop para todas las conexiones de PolyBase a clústeres de Hadoop o almacenamiento de blobs de Azure (WASB). Esta configuración es necesaria para crear un origen de datos externo para una tabla externa. Para obtener más información, vea [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 Esta es la configuración de conectividad de Hadoop y sus orígenes de datos de Hadoop compatibles correspondientes. Solo puede estar en vigor un valor de cada vez. Las opciones 1, 4 y 7 permiten que se creen y usen varios tipos de orígenes de datos externos en todas las sesiones en el servidor.  
  
-   Opción 0: deshabilitar la conectividad de Hadoop  
  
-   Opción 1: Hortonworks HDP 1.3 en Windows Server  
  
-   Opción 1: almacenamiento de blobs de Azure (WASB[S])  
  
-   Opción 2: Hortonworks HDP 1.3 en Linux  
  
-   Opción 3: Cloudera CDH 4.3 en Linux  
  
-   Opción 4: Hortonworks HDP 2.0 en Windows Server  
  
-   Opción 4: almacenamiento de blobs de Azure (WASB[S])  
  
-   Opción 5: Hortonworks HDP 2.0 en Linux  
  
-   Opción 6: Cloudera 5.1, 5.2, 5.3, 5.4, 5.5, 5.9, 5.10, 5.11, 5.12 y 5.13 en Linux  
  
-   Opción 7: Hortonworks 2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 3.0 en Linux  
  
-   Opción 7: Hortonworks 2.1, 2.2 y 2.3 en Windows Server  
  
-   Opción 7: almacenamiento de blobs de Azure (WASB[S])  
  
 **RECONFIGURE**  
 Actualiza el valor de ejecución (run_value) para que coincida con el valor de configuración (config_value). Vea [Conjuntos de resultados](#ResultSets) para obtener definiciones de run_value y config_value. El nuevo valor de configuración que se establece mediante sp_configure no es efectivo hasta que se establezca el valor de ejecución mediante la instrucción RECONFIGURE.  
  
 Tras ejecutar RECONFIGURE, debe detener y reiniciar el servicio de SQL Server. Tenga en cuenta que, al detener el servicio de SQL Server, los dos motores PolyBase adicionales y el servicio de movimiento de datos se detendrán automáticamente. Después de reiniciar el servicio de motor de SQL Server, vuelva a iniciar estos dos servicios de nuevo (no se inician automáticamente).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
##  <a name="ResultSets"></a> Conjuntos de resultados  
 Cuando se ejecuta sin parámetros, **sp_configure** devuelve un conjunto de resultados con cinco columnas.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|Nombre de la opción de configuración.|  
|**Mínimo**|**int**|Valor mínimo de la opción de configuración.|  
|**Máximo**|**int**|Valor máximo de la opción de configuración.|  
|**config_value**|**int**|Valor que se ha configurado con **sp_configure**.|  
|**run_value**|**int**|Valor actual en uso por PolyBase. Este valor se establece al ejecutar RECONFIGURE.<br /><br /> Los valores **config_value** y **run_value** son normalmente los mismos, a menos que el valor se esté modificando.<br /><br /> Si la reconfiguración está en curso, podría ser necesario reiniciar antes de que este valor de ejecución sea preciso.|  
  
## <a name="general-remarks"></a>Notas generales  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], después de volver a ejecutar RECONFIGURE, para que surta efecto el valor de ejecución de la “conectividad de Hadoop”, debe reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
En [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], después de volver a ejecutar RECONFIGURE, para que surta efecto el valor de ejecución de la “conectividad de Hadoop”, debe reiniciar la región de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 RECONFIGURE no se permite en una transacción implícita o explícita.  
  
## <a name="permissions"></a>Permisos  
 Todos los usuarios pueden ejecutar **sp_configure** sin parámetros o con el parámetro @configname .  
  
 Requiere permiso a nivel de servidor de **ALTER SETTINGS** o la pertenencia al rol fijo de servidor **sysadmin** para cambiar un valor de configuración o para ejecutar RECONFIGURE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-list-all-available-configuration-settings"></a>A. Lista de todas las opciones de configuración disponibles  
 En este ejemplo se muestra cómo enumerar todas las opciones de configuración.  
  
```  
EXEC sp_configure;  
```  
  
 El resultado devuelve el nombre de opción seguido por los valores mínimo y máximo de la opción. El valor **config_value** es el valor que usarán SQL o PolyBase al completar la reconfiguración. El valor **run_value** es el valor que se está usando actualmente. Los valores **config_value** y **run_value** son normalmente los mismos, a menos que el valor se esté modificando.  
  
### <a name="b-list-the-configuration-settings-for-one-configuration-name"></a>B. Lista de las opciones de configuración para un nombre de configuración  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="c-set-hadoop-connectivity"></a>C. Establecer la conectividad de Hadoop  
 Este ejemplo establece PolyBase a la opción 7. Esta opción permite que PolyBase cree y use tablas externas en Hortonworks 2.1, 2.2 y 2.3 en Linux y Windows Server y en el almacenamiento de blobs de Azure. Por ejemplo, SQL podría tener 30 tablas externas con 7 de ellas haciendo referencia a datos en Hortonworks 2.1 en Linux, 4 en Hortonworks 2.2 en Linux, 7 en Hortonworks 2.3 en Linux y las otras 12 haciendo referencia al almacenamiento de blobs de Azure.  
  
```  
--Configure external tables to reference data on Hortonworks 2.1, 2.2, and 2.3 on Linux, and Azure blob storage  
  
sp_configure @configname = 'hadoop connectivity', @configvalue = 7;  
GO  
  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
