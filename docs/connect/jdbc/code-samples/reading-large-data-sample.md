---
title: Leer datos de gran tamaño ejemplo | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d75c6fcf4148a4aa27dee51300d41a8c42e80acf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32830060"
---
# <a name="reading-large-data-sample"></a>Leer un ejemplo de datos grandes
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esto [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicación de ejemplo muestra cómo recuperar un valor de columna única grande desde un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos mediante la [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) método.  
  
 El archivo de código para este ejemplo se llama readLargeData.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación de*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\adaptive  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, necesitará acceso a la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. También deberá establecer la ruta de clase para incluir el archivo sqljdbc.jar o el archivo sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc.jar o sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". Para obtener más información sobre cómo establecer la ruta de clase, consulte [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona sqljdbc.jar y sqljdbc4.jar los archivos de biblioteca de clases que se usan según su configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el código de ejemplo realiza una conexión a la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos. Luego, el código muestra crea los datos del ejemplo y actualiza la tabla Production.Document con una consulta con parámetros.  
  
 Además, el código de ejemplo muestra cómo obtener el modo de almacenamiento en búfer adaptable usando la [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) método de la [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) clase. Tenga en cuenta que desde la publicación de la versión 2.0 del controlador JDBC, la propiedad de conexión responseBuffering se establece en "adaptive" de manera predeterminada.  
  
 A continuación, usar una instrucción SQL con el [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) de objeto, el código de ejemplo ejecuta la instrucción SQL y coloca los datos que devuelve en una [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
 Por último, el código de ejemplo recorre en iteración las filas de datos que se encuentran en el conjunto de resultados y utiliza el [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) método para tener acceso a algunos de los datos que contiene.  
  
 [!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Trabajo con datos grandes](../../../connect/jdbc/working-with-large-data.md)  
  
  
