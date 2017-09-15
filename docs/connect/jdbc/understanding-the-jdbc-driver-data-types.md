---
title: "Descripción de los tipos de datos del controlador JDBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1cd9f516a8d72aabf8b10d25b9553cf35a3be3bd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-the-jdbc-driver-data-types"></a>Describir los tipos de datos del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]admite el uso de tipos de datos básicos y avanzados de JDBC dentro de una aplicación de Java que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como su base de datos.  
  
 El sistema de tipos JDBC arbitra la conversión entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos y tipos del lenguaje Java y objetos. Los tipos de JDBC se modelan en los tipos SQL-92 y SQL-99. El controlador JDBC sigue la especificación de JDBC y está diseñado para proporcionar un equilibrio correcto derecho entre previsibilidad y flexibilidad.  
  
 En los temas de esta sección se describe cómo utilizar los tipos de datos básicos y avanzados, y cómo se pueden convertir en otros tipos de datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Uso de tipos de datos básicos](../../connect/jdbc/using-basic-data-types.md)|Describe los tipos de datos básicos de JDBC. Incluye ejemplos de cómo trabajar con los tipos de datos utilizando conjuntos de resultados, consultas parametrizadas y procedimientos almacenados.|  
|[Configurar cómo los valores java.sql.Time se envían al servidor](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)|Describe cómo el controlador JDBC genera fechas.|  
|[Uso de tipos de datos avanzados](../../connect/jdbc/using-advanced-data-types.md)|Describe los tipos de datos avanzados de JDBC.|  
|[Diferencias de tipos de datos](../../connect/jdbc/understanding-data-type-differences.md)|Describe las diferencias entre los diversos tipos de datos del controlador JDBC.|  
|[Conversiones de tipos de datos de descripción](../../connect/jdbc/understanding-data-type-conversions.md)|Describe cómo se administra la conversión de tipos de datos cuando se usan métodos establecedor y captador.|  
|[Compatibilidad con juego de caracteres nacionales](../../connect/jdbc/national-character-set-support.md)|Describe la compatibilidad con los tipos del juego de caracteres nacionales.|  
|[Compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md)|Describe la interfaz SQLXML. También se describe cómo leer y escribir datos XML desde y hacia la base de datos relacional con el **SQLXML** tipo de datos de Java.|  
|[Contenedores e Interfaces](../../connect/jdbc/wrappers-and-interfaces.md)|Describe las interfaces que tienen la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] determinados métodos y constantes que permiten a un servidor de aplicaciones crear un proxy de la clase, también se tratan admite para la interfaz java.sql.Wrapper.|  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre el controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
