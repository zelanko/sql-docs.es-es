---
title: Consideraciones básicas de seguridad de SQLXML
description: Obtenga información sobre las directrices de seguridad principales para usar SQLXML para el acceso a datos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- security [SQLXML], about security
ms.assetid: 330cd2ff-d5d5-4c8e-8f93-0869c977be94
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 40f3ef6735bb2de27fd4fda07c3f508717f52515
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790685"
---
# <a name="core-sqlxml-security-considerations"></a>Consideraciones básicas de seguridad de SQLXML
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  A continuación se indican instrucciones de seguridad para utilizar SQLXML en el acceso a datos.  
  
-   El proveedor SQLXMLOLEDB expone una propiedad **StreamFlags** que le permite establecer marcas que indican qué funcionalidad SQLXML debe estar habilitada o deshabilitada para cada instancia específica. Puede utilizar esta propiedad para personalizar el uso de SQLXML y asegurarse de que solo se habilitan los componentes que desea. Para obtener más información, vea [proveedor SQLXMLOLEDB &#40;SQLXML 4,0&#41;](https://msdn.microsoft.com/library/fc489682-690a-4bb0-b5ac-237d376dc110).  
  
-   Cuando se producen y se devuelven errores SQLXML, pueden incluir información sobre el esquema de la base de datos como nombres de tabla, nombres de columna o información de tipo. Debe tener cuidado al controlar estos errores para que los usuarios no puedan detectar fácilmente la información sobre la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde no esté previsto ni sea necesario.  
  
-   Cuando se utiliza para consultar o enviar actualizaciones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], SQLXML no establece ningún límite en la cantidad de datos que se pueden intercambiar y no realiza ninguna comprobación sobre el tamaño de los datos en una carga SQLXML antes de intentar procesarla. Al desarrollar la aplicación con SQLXML, debe asegurarse de que existe suficiente memoria en el sistema para procesar los datos. Por ejemplo, al consultar datos del servidor, debe comprobar que existe suficiente espacio en memoria en el cliente para recibirlos. De la misma forma, si carga los datos en el servidor, debe comprobar que existe suficiente memoria disponible en el servidor para procesarlos y suficiente espacio de almacenamiento en disco disponible en el servidor para almacenar los datos.  
  
-   SQLXML genera dinámicamente consultas y comandos de actualización [!INCLUDE[tsql](../../../includes/tsql-md.md)] y los envía a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la ejecución. Ésta es la única manera en la que SQLXML consulta y actualiza el servidor. Los resultados se reciben como un flujo (de XML) o como un conjunto de filas.  
  
-   Al recibir los resultados de la consulta, SQLXML no toma ninguna medida basada en el contenido de los datos que recibe. No se realiza ningún procesamiento adicional basado en el tipo ni el contenido de los datos. Los datos nunca se tratan como código con el que ejecutar acciones.  
  
-   Al ejecutar plantillas XML, SQLXML traduce las consultas DBOBJECT y XPath incluidas en la plantilla enviada en comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] que posteriormente se ejecutan en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Estos comandos solo afectan a datos existentes. Los comandos que genera SQLXML nunca modifican la estructura de la base de datos. Los usuarios deben ejecutar comandos explícitos para modificar la estructura de la base de datos. Por ejemplo, incluyéndolos en un bloque **SQL: query** de una plantilla.  
  
-   Al ejecutar consultas DBOBJECT e instrucciones XPath en los archivos de asignación, SQLXML no modifica de forma alguna los datos de la base de datos.  
  
-   SQLXML puede realizar cambios de formato en los datos proporcionados basándose en las diferencias entre los modelos de datos XML y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por ejemplo, el formato para especificar una hora es distinto. SQLXML intentará resolver estas diferencias. Como resultado, es posible que se pierdan algunos datos de precisión.  
  
-   SQLXML no establece ningún límite en la cantidad de tiempo que tarda en procesar los datos. El procesamiento continuará hasta que se produzca un error o se complete el procesamiento.  
  
-   SQLXML no escribe en el sistema de archivos. Si los usuarios desean guardar los datos que recuperan de la base de datos, deben hacerlo en el código.  
  
-   SQLXML permite a los usuarios ejecutar cualquier consulta SQL que deseen en la base de datos. Esta funcionalidad nunca se debe exponer a un origen sin seguridad ni control, ya que básicamente se abre la base de datos SQL a cualquier usuario sin ninguna disposición.  
  
-   Al ejecutar diagramas, SQLXML traduce los bloques **atributo updg: Sync** en comandos DELETE, Update e Insert en la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia de. Estos comandos solo afectan a datos existentes. Los comandos que genera SQLXML nunca modifican la base de datos. Los usuarios deben ejecutar comandos explícitos para modificar la estructura de la base de datos. Por ejemplo, incluyéndolos en un bloque **SQL: query** de una plantilla.  
  
-   Al ejecutar DiffGrams, SQLXML traduce los DiffGrams en comandos DELETE, UPDATE e INSERT en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Estos comandos solo afectan a datos existentes. Los comandos que genera SQLXML nunca modifican la base de datos. Los usuarios deben ejecutar comandos explícitos para modificar la estructura de la base de datos. Por ejemplo, incluyéndolos en un bloque **SQL: query** de una plantilla.  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de seguridad de SQLXML 4.0](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
  
  
