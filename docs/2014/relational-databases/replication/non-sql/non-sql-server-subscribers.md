---
title: Suscriptores que no sean de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- heterogeneous data sources, non-SQL Server Subscribers
- heterogeneous data sources
- heterogeneous database replication, non-SQL Server Subscribers
- non-SQL Server Subscribers, about non-SQL Server Subscribers
- heterogeneous Subscribers
- heterogeneous Subscribers, about heterogeneous Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers
ms.assetid: 831e7586-2949-4b9b-a2f3-7b0b699b23ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3b1f285243e2b925cca9d263a53c9b70087ea5d4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068589"
---
# <a name="non-sql-server-subscribers"></a>suscriptores que no son de SQL Server
  Los siguientes suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden suscribirse a publicaciones de instantáneas y transaccionales mediante suscripciones de inserción. Las suscripciones se admiten en las dos versiones más recientes de cada base de datos enumerada utilizando la versión más reciente del proveedor OLE DB indicado.  
  
 La replicación heterogénea en suscriptores que no son SQL Server está desusada. La publicación de Oracle está desusada. Para mover datos, cree soluciones mediante captura de datos modificados y [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
|Base de datos|Sistema operativo|Proveedor|  
|--------------|----------------------|--------------|  
|Oracle|Todas las plataformas que admite Oracle|Proveedor OLE DB de Oracle (suministrado por Oracle)|  
|IBM DB2|MVS, AS400, Unix, Linux, Windows excepto 9.x|Proveedor OLE DB de Microsoft Host Integration Server (HIS)|  
  
 Para obtener información acerca de cómo crear suscripciones a Oracle e IBM DB2, vea [suscriptores de Oracle](oracle-subscribers.md) y [IBM DB2 Subscribers](ibm-db2-subscribers.md).  
  
## <a name="considerations-for-non-sql-server-subscribers"></a>Consideraciones para suscriptores que no son de SQL Server  
 Tenga en cuenta las siguientes consideraciones al replicar datos en suscriptores que no sean de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
### <a name="general-considerations"></a>Consideraciones generales  
  
-   La replicación es compatible con la publicación de tablas y vistas indizadas como tablas en suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (las vistas indizadas no se pueden replicar como vistas indizadas).  
  
-   Al crear una publicación en el Asistente para nueva publicación y habilitarla para suscriptores que no son de SQL Server mediante el cuadro de diálogo Propiedades de la publicación, el propietario de todos los objetos de la base de datos de suscripciones no se especifica para los suscriptores que no son de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mientras que para los [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suscriptores se establece en el propietario del objeto correspondiente de la base de datos de publicación  
  
-   Si una publicación va a tener suscriptores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se debe habilitar la publicación para los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de crear cualquier suscripción a suscriptores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   De manera predeterminada, los scripts generados por el Agente de instantáneas para los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizan identificadores sin comillas en la sintaxis CREATE TABLE. Por lo tanto, una tabla publicada denominada 'test' se replica como 'TEST'. Para usar mayúsculas y minúsculas como en la tabla de la base de datos de publicación, utilice el parámetro **-QuotedIdentifier** para el Agente de distribución. También se debe utilizar el parámetro **-QuotedIdentifier** si los nombres de objeto publicados (como tablas, columnas y restricciones) contienen espacios o palabras que son palabras reservadas en la versión de la base de datos de suscriptor que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información acerca de este parámetro, vea [Agente de distribución de replicación](../agents/replication-distribution-agent.md).  
  
-   La cuenta con la que se ejecuta el agente de distribución debe tener acceso de lectura en el directorio de instalación del proveedor OLE DB.  
  
-   De manera predeterminada para los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el Agente de distribución utiliza el valor [(destino predeterminado)] para la base de datos de suscripciones (el parámetro **-SubscriberDB** del Agente de distribución):  
  
    -   En Oracle, un servidor tiene como máximo una base de datos, por lo que no es necesario especificarla.  
  
    -   En IBM DB2, la base de datos se especifica en la cadena de conexión DB2. Para más información, consulte [Crear una suscripción para un suscriptor que no sea de SQL Server](../create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
-   Si el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta en una plataforma de 64 bits, debe usar la versión de 64 bits del proveedor OLE DB apropiado.  
  
-   La replicación mueve los datos en formato Unicode con independencia de las páginas de intercalación/códigos utilizadas en el publicador y el suscriptor. Se recomienda elegir una página de intercalación/códigos compatible al replicar entre publicadores y suscriptores.  
  
-   Si se agrega o elimina un artículo de una publicación, se deben reinicializar las suscripciones a suscriptores que no sean de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Las únicas restricciones que admiten los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] son: NULL y NOT NULL. Las restricciones de clave principal se replican como índices únicos.  
  
-   El valor NULL se trata de manera distinta en diferentes bases de datos y esto afecta al modo de representar un valor en blanco, una cadena vacía y un valor NULL. A su vez, afecta al comportamiento de los valores insertados en columnas con restricciones únicas definidas. Por ejemplo, Oracle permite varios valores NULL en una columna considerada única, mientras que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo permite un valor NULL en una columna única.  
  
     Otro factor es cómo se tratan los valores NULL, las cadenas vacías y los valores en blanco cuando se define la columna como NOT NULL. Para obtener información acerca de cómo tratar este problema en suscriptores de Oracle, vea [suscriptores de Oracle](oracle-subscribers.md).  
  
-   Los metadatos relacionados con la replicación (tabla de secuencias de transacciones) no se elimina de los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando se quita la suscripción.  
  
### <a name="conforming-to-the-requirements-of-the-subscriber-database"></a>Cumplir los requisitos de la base de datos de suscriptor  
  
-   El esquema y los datos publicados deben respetar los requisitos de la base de datos en el suscriptor. Por ejemplo, si una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene un tamaño de fila máximo menor que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], debe asegurarse de que el esquema y los datos publicados no superen dicho tamaño.  
  
-   Las tablas replicadas en suscriptores que no sean de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adoptarán las convenciones de nomenclatura de tablas de la base de datos en el suscriptor.  
  
-   DDL no se admite para suscriptores que no sean de SQL Server. Para obtener más información sobre los cambios de esquema, vea [Realizar cambios de esquema en bases de datos de publicaciones](../publish/make-schema-changes-on-publication-databases.md).  
  
### <a name="replication-feature-support"></a>Compatibilidad con la característica de replicación  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ofrece dos tipos de suscripciones: de inserción y de extracción. Los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deben utilizar suscripciones de inserción, en las que el Agente de distribución se ejecuta en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona dos formatos de instantánea: modo bcp nativo y modo de carácter. Los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requieren instantáneas en modo de carácter.  
  
-   Los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no pueden utilizar suscripciones de actualización inmediata o actualización en cola, ni ser nodos en una topología punto a punto.  
  
-   Los suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se pueden inicializar automáticamente desde una copia de seguridad.  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de base de datos heterogénea](heterogeneous-database-replication.md)   
 [Subscribe to Publications](../subscribe-to-publications.md)  
  
  
