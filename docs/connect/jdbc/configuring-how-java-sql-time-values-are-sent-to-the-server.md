---
title: Configurar el modo en que los valores java.sql.Time se envían al servidor | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0f359c66250d11fa01c74567e1faeab3ff064ac
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602255"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurar el modo en que los valores java.sql.Time se envían al servidor
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Si usa un objeto java.sql.Time o el tipo de JDBC java.sql.Types.TIME para establecer un parámetro, podrá configurar la forma en que el valor java.sql.Time se envía al servidor; es decir, como un tipo **time** o un tipo **datetime** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Este escenario se aplica al utilizar uno de los siguientes métodos:  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 Puede configurar la forma de enviar el valor java.sql.Time mediante el uso de la propiedad de conexión **sendTimeAsDatetime**. Para obtener más información, vea [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Puede modificar mediante programación el valor de la propiedad de conexión **sendTimeAsDatetime** con [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] no son compatibles con el **tiempo** como los valores de tipo de datos, por lo que las aplicaciones que usen java.sql.Time por lo general almacenan java.sql.Time **datetime** o **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.  
  
 Si desea usar el **datetime** y **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos cuando se trabaja con los valores java.sql.Time, debería establecer el **sendTimeAsDatetime** propiedad de conexión en **true**. Si desea usar el **tiempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del tipo de datos cuando trabaje con valores java.sql.Time, debería establecer el **sendTimeAsDatetime** propiedad de conexión en **false**.  
  
 Tenga en cuenta que al enviar valores java.sql.Time a un parámetro cuyo tipo de datos también pueda almacenar fechas, esos valores predeterminados de fecha serán distintos en función de si el valor java.sql.Time se envía como un valor **datetime** (1/1/1970) o un valor **time** (1/1/1900). Para más información sobre las conversiones de datos al enviar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Usar datos de fecha y hora](https://go.microsoft.com/fwlink/?LinkID=145211).  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador JDBC 3.0, **sendTimeAsDatetime** es true de forma predeterminada. En versiones futuras, la propiedad de conexión **sendTimeAsDatetime** puede establecerse de forma predeterminada en False.  
  
 Para asegurarse de que su aplicación sigue funcionando como se había previsto independientemente del valor predeterminado de la propiedad de conexión **sendTimeAsDatetime**, puede:  
  
-   Usar java.sql.Time al trabajar con el tipo de datos **time** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizar java.sql.Timestamp al trabajar con el **datetime**, **smalldatetime**, y **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.  
  
SendTimeAsDatetime debe ser false para las columnas cifradas como las columnas cifradas no son compatibles con la conversión de tiempo a la fecha y hora. Desde Microsoft JDBC Driver 6.0 para SQL Server, la clase SQLServerConnection tiene los dos métodos siguientes para establecer y obtener el valor de la propiedad sendTimeAsDatetime.

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Ver también  
 [Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
