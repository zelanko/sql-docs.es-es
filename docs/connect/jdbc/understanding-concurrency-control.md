---
title: Descripción del control de la simultaneidad | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3cbc805ece4cc28a646d93d6607bcc45d65cd563
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027646"
---
# <a name="understanding-concurrency-control"></a>Descripción del control de la simultaneidad
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El control de la simultaneidad se refiere a las diversas técnicas que se utilizan para conservar la integridad de la base de datos cuando varios usuarios actualizan filas al mismo tiempo. Una simultaneidad incorrecta puede causar problemas, como la lectura de datos sucios, las lecturas fantasmas y las lecturas no repetibles. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona interfaces para todas las técnicas de simultaneidad que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emplea para resolver estos problemas.  
  
> [!NOTE]  
>  Para obtener más información sobre la simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "Administrar el acceso simultáneo a datos" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Observaciones  
 El controlador JDBC es compatible con los tipos de simultaneidad siguientes:  
  
|Tipo de simultaneidad|Características|Bloqueos de fila|Descripción|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|Solo lectura|No|No se permiten las actualizaciones a través del cursor y no se mantienen los bloqueos en las filas que forman el conjunto de resultados.|  
|CONCUR_UPDATABLE|Lectura-escritura optimista|No|La base de datos supone que la contención de la fila es improbable, pero posible. La integridad de las filas se comprueba con una comparación de la marca de tiempo.|  
|CONCUR_SS_SCROLL_LOCKS|Lectura-escritura pesimista|Sí|La base de datos supone que la contención de la fila es probable. La integridad de la fila se garantiza con el bloqueo de filas.|  
|CONCUR_SS_OPTIMISTIC_CC|Lectura-escritura optimista|No|La base de datos supone que la contención de la fila es improbable, pero posible. La integridad de las filas se comprueba con una comparación de la marca de tiempo.<br /><br /> En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, el servidor cambiará esto por CONCUR_SS_OPTIMISTIC_CCVAL si la tabla no contiene una columna de marca de tiempo.<br /><br /> En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], si la tabla subyacente tiene una columna de marca de tiempo, se utiliza OPTIMISTIC WITH ROW VERSIONING incluso si se especifica OPTIMISTIC WITH VALUES. Si se especifica OPTIMISTIC WITH ROW VERSIONING y la tabla no incluye marcas de tiempo, se utiliza OPTIMISTIC WITH VALUES.|  
|CONCUR_SS_OPTIMISTIC_CCVAL|Lectura-escritura optimista|No|La base de datos supone que la contención de la fila es improbable, pero posible. La integridad de las filas se comprueba con una comparación de los datos de las filas.|  
  
## <a name="result-sets-that-are-not-updateable"></a>Conjuntos de resultados que no son actualizables  
 Un conjunto de resultados actualizable es aquel en el que las filas se pueden insertar, actualizar y eliminar. En los casos siguientes, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede crear un cursor actualizable. La excepción que se genera es: "El conjunto de resultados no es actualizable".  
  
|Causa|Descripción|Solución|  
|-----------|-----------------|------------|  
|La instrucción no se crea con la sintaxis de JDBC 2.0 (o versiones posteriores)|JDBC 2.0 introdujo métodos nuevos para crear instrucciones. Si se usa la sintaxis de JDBC 1.0, el conjunto de resultados se establece de forma predeterminada como de solo lectura.|Especifique el tipo del conjunto de resultados y la simultaneidad al crear la instrucción.|  
|La instrucción se crea con TYPE_SCROLL_INSENSITIVE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un cursor de instantánea estático. Se desconecta de las filas de la tabla subyacente para ayudar a proteger el cursor de las actualizaciones de filas de otros usuarios.|Use TYPE_SCROLL_SENSITIVE, TYPE_SS_SCROLL_KEYSET, TYPE_SS_SCROLL_DYNAMIC o TYPE_FORWARD_ONLY con CONCUR_UPDATABLE para evitar crear un cursor estático.|  
|El diseño de la tabla imposibilita el uso de un cursor KEYSET o DYNAMIC|La tabla subyacente no tiene claves únicas para habilitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que identifique de forma única una fila.|Agregue claves únicas a la tabla para permitir la identificación exclusiva de cada fila.|  
  
## <a name="see-also"></a>Consulte también  
 [Administración de conjuntos de resultados con el controlador JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
