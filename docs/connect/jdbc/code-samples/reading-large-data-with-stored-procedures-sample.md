---
title: Leer datos grandes con un ejemplo de procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcbeba3d535450001c15ab3168df9da59f7dceb2
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279037"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Leer datos grandes con un ejemplo de procedimientos almacenados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo recuperar un parámetro OUT grande desde un procedimiento almacenado.  
  
 El archivo de código para este ejemplo se denomina ExecuteStoredProcedure.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\adaptive  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, deberá tener acceso a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. También establece la ruta de clase para incluir el archivo jar de mssql-jdbc. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
 Cree el siguiente procedimiento almacenado en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]:  
  
```sql
CREATE PROCEDURE GetLargeDataValue   
  (@Document_ID int,   
   @Document_ID_out int OUTPUT,   
   @Document_Title varchar(50) OUTPUT,  
   @Document_Summary nvarchar(max) OUTPUT)  
  
AS   
BEGIN    
   SELECT @Document_ID_out = DocumentID,   
          @Document_Title = Title,  
          @Document_Summary = DocumentSummary   
    FROM  Production.Document  
    WHERE DocumentID = @Document_ID  
END  
```  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, el código realiza una conexión a la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Luego, el código muestra crea los datos del ejemplo y actualiza la tabla Production.Document con una consulta con parámetros. Después, el código establece el modo de almacenamiento en búfer adaptable con el método [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) y ejecuta el procedimiento almacenado GetLargeDataValue. Tenga en cuenta que desde la publicación de la versión 2.0 del controlador JDBC, la propiedad de conexión responseBuffering se establece en "adaptive" de manera predeterminada.  
  
 Finalmente, el código muestra los datos devueltos con los parámetros OUT y cómo usar los métodos `mark` y `reset` en el flujo para volver a leer cualquier parte de los datos.  
  
 [!code[JDBC#UsingAdaptiveBuffering2](../../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]  
  
## <a name="see-also"></a>Ver también  
 [Trabajo con datos grandes](../../../connect/jdbc/working-with-large-data.md)  
  
  
