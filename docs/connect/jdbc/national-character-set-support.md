---
title: Compatibilidad con juego de caracteres nacional | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f143d37911a1375a1eebe9de04c8b509817575ec
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="national-character-set-support"></a>Compatibilidad con juego de caracteres nacionales
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El controlador JDBC proporciona compatibilidad con la API de JDBC 4.0, que incluye nuevos métodos de la API de conversión de juegos de caracteres nacionales. Esta compatibilidad incluye nuevos métodos establecedor, captador y actualizador para **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, y **NCLOB** tipos de JDBC.  
  
 A continuación se incluye una lista de nuevos métodos captador, establecedor y actualizador que permiten la conversión al juego de caracteres nacionales:  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md).  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md), [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md).  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md), [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md), [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md), [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md).  
  
> [!NOTE]  
>  Para usar estos métodos en su aplicación, debe establecer la ruta de clase para incluir el archivo sqljdbc4.jar.  
  
 Para enviar formatos String al servidor en formato Unicode, las aplicaciones deben usar los nuevos métodos de caracteres nacionales de JDBC 4.0; o establezca la **sendStringParametersAsUnicode** propiedad de conexión en "**true**" al utilizar los métodos de caracteres nacionales. Lo recomendable es usar los nuevos métodos de caracteres nacionales de JDBC 4.0 cuando sea posible. Para obtener más información sobre la **sendStringParametersAsUnicode** propiedad de conexión, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

