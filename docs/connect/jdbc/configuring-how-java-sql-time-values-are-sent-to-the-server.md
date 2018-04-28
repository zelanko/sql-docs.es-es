---
title: Configurar cómo se envían los valores java.sql.Time al servidor | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4550251e0b768c3be17b6efbbac43f8b6618dcf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurar el modo en que los valores java.sql.Time se envían al servidor
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Si utilizas un objeto java.sql.Time o el tipo de JDBC java.sql.Types.TIME para establecer un parámetro, puede configurar la forma en que el valor java.sql.Time se envía al servidor; como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tiempo** tipo o como un **datetime** tipo.  
  
 Este escenario se aplica al utilizar uno de los siguientes métodos:  
  
-   [SQLServerCallableStatement.registerOutParameter (int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter (int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 Puede configurar cómo se envía el valor java.sql.Time mediante el **sendTimeAsDatetime** propiedad de conexión. Para obtener más información, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Puede modificar mediante programación el valor de la **sendTimeAsDatetime** propiedad de conexión con [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] no admiten la **tiempo** los valores de tipo de datos, por lo que las aplicaciones que usen java.sql.Time por lo general almacenan java.sql.Time como **datetime** o **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos.  
  
 Si desea utilizar el **datetime** y **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos cuando se trabaja con valores java.sql.Time, debería establecer la **sendTimeAsDatetime** propiedad de conexión en **true**. Si desea utilizar el **tiempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de tipos de datos cuando trabaje con valores java.sql.Time, debería establecer la **sendTimeAsDatetime** propiedad de conexión en **false**.  
  
 Tenga en cuenta que al enviar valores java.sql.Time a un parámetro cuyo tipo de datos también puede almacenar fechas, esos valores predeterminados de fecha son diferentes dependiendo de si el valor java.sql.Time se envía como un **datetime** (1/1/1970) o **tiempo** valor (1/1/1900). Para obtener más información acerca de las conversiones de datos al enviar datos a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [utilizando datos de fecha y hora](http://go.microsoft.com/fwlink/?LinkID=145211).  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] controlador JDBC 3.0, **sendTimeAsDatetime** es true de forma predeterminada. En versiones futuras, la **sendTimeAsDatetime** propiedad de conexión se puede establecer en false de forma predeterminada.  
  
 Para asegurarse de que su aplicación sigue funcionando según lo previsto independientemente del valor predeterminado de la **sendTimeAsDatetime** propiedad de conexión, puede:  
  
-   Utilizar java.sql.Time al trabajar con el **tiempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos.  
  
-   Utilizar java.sql.Timestamp al trabajar con el **datetime**, **smalldatetime**, y **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos.  
  
Tenga en cuenta que sendTimeAsDatetime debe ser false para las columnas cifradas como columnas cifradas no admiten la conversión de hora a fecha y hora. Comenzar con Microsoft JDBC Driver 6.0 para SQL Server, la clase SQLServerConnection tiene los dos métodos siguientes para el valor de la propiedad sendTimeAsDatetime set/get.

```
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Vea también  
 [Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
