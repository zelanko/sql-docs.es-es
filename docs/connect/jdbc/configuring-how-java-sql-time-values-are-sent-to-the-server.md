---
title: Configuración del modo en que los valores java.sql.Time se envían al servidor | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fe6969d51834d0798a530b9cc9926af1b27fec2
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028233"
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
  
 Las versiones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de anteriores [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] a no admiten el tipo de datos **Time** , por lo que las aplicaciones que usan Java. SQL. Time normalmente almacenan los valores Java. SQL. Time como tipos de datos **DateTime** o **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Si desea utilizar los tipos de datos **DateTime** y **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al trabajar con valores Java. SQL. Time, debe establecer la propiedad de conexión **sendTimeAsDatetime** en **true**. Si desea utilizar el tipo de datos **Time** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al trabajar con valores Java. SQL. Time, debe establecer la propiedad de conexión **sendTimeAsDatetime** en **false**.  
  
 Tenga en cuenta que al enviar valores java.sql.Time a un parámetro cuyo tipo de datos también pueda almacenar fechas, esos valores predeterminados de fecha serán distintos en función de si el valor java.sql.Time se envía como un valor **datetime** (1/1/1970) o un valor **time** (1/1/1900). Para más información sobre las conversiones de datos al enviar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Usar datos de fecha y hora](https://go.microsoft.com/fwlink/?LinkID=145211).  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el controlador JDBC 3,0, **sendTimeAsDatetime** es true de forma predeterminada. En versiones futuras, la propiedad de conexión **sendTimeAsDatetime** puede establecerse de forma predeterminada en False.  
  
 Para asegurarse de que su aplicación sigue funcionando como se había previsto independientemente del valor predeterminado de la propiedad de conexión **sendTimeAsDatetime**, puede:  
  
-   Usar java.sql.Time al trabajar con el tipo de datos **time** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Use Java. SQL. timestamp al trabajar con los tipos de datos **DateTime**, **smalldatetime**y **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
SendTimeAsDatetime debe ser false para las columnas cifradas, ya que las columnas cifradas no admiten la conversión de Time a DateTime. A partir de Microsoft JDBC driver 6,0 para SQL Server, la clase SQLServerConnection tiene los dos métodos siguientes para establecer u obtener el valor de la propiedad sendTimeAsDatetime.

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Vea también
 [Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
