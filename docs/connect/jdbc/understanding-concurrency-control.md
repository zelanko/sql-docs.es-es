---
title: Descripción del Control de simultaneidad | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71ca87537cef389ac6cedb47b21a39ce76ba1b97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853220"
---
# <a name="understanding-concurrency-control"></a>Descripción del control de la simultaneidad
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El control de la simultaneidad se refiere a las diversas técnicas que se utilizan para conservar la integridad de la base de datos cuando varios usuarios actualizan filas al mismo tiempo. Una simultaneidad incorrecta puede causar problemas, como la lectura de datos sucios, las lecturas fantasmas y las lecturas no repetibles. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona interfaces para todas las técnicas de simultaneidad usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para resolver estos problemas.  
  
> [!NOTE]  
>  Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] simultaneidad, vea "Administrar acceso simultáneo a datos" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="remarks"></a>Comentarios  
 El controlador JDBC es compatible con los tipos de simultaneidad siguientes:  
  
|Tipo de simultaneidad|Características|Bloqueos de fila|Description|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|Solo lectura|no|No se permiten las actualizaciones a través del cursor y no se mantienen los bloqueos en las filas que forman el conjunto de resultados.|  
|CONCUR_UPDATABLE|Lectura-escritura optimista|no|La base de datos supone que la contención de la fila es improbable, pero posible. La integridad de las filas se comprueba con una comparación de la marca de tiempo.|  
|CONCUR_SS_SCROLL_LOCKS|Lectura-escritura pesimista|Sí|La base de datos supone que la contención de la fila es probable. La integridad de la fila se garantiza con el bloqueo de filas.|  
|CONCUR_SS_OPTIMISTIC_CC|Lectura-escritura optimista|no|La base de datos supone que la contención de la fila es improbable, pero posible. Se comprueba la integridad de las filas con una comparación de marca de tiempo.<br /><br /> Para [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] y versiones posteriores, el servidor cambiará esto por concur_ss_optimistic_ccval si la tabla no contiene una columna de marca de tiempo.<br /><br /> Para [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], si la tabla subyacente tiene una columna de marca de tiempo, se utiliza OPTIMISTIC WITH ROW VERSIONING incluso si se especifica OPTIMISTIC WITH VALUES. Si se especifica OPTIMISTIC WITH ROW VERSIONING y la tabla no incluye marcas de tiempo, se utiliza OPTIMISTIC WITH VALUES.|  
|CONCUR_SS_OPTIMISTIC_CCVAL|Lectura-escritura optimista|no|La base de datos supone que la contención de la fila es improbable, pero posible. La integridad de las filas se comprueba con una comparación de los datos de las filas.|  
  
## <a name="result-sets-that-are-not-updateable"></a>Conjuntos de resultados que no son actualizables  
 Un conjunto de resultados actualizable es aquel en el que las filas se pueden insertar, actualizar y eliminar. En los casos siguientes, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no se puede crear un cursor actualizable. La excepción que se genera es: "El conjunto de resultados no es actualizable".  
  
|Causa|Description|Remedy|  
|-----------|-----------------|------------|  
|La instrucción no se crea con la sintaxis de JDBC 2.0 (o versiones posteriores)|JDBC 2.0 introdujo métodos nuevos para crear instrucciones. Si se usa la sintaxis de JDBC 1.0, el conjunto de resultados se establece de forma predeterminada como de solo lectura.|Especifique el tipo del conjunto de resultados y la simultaneidad al crear la instrucción.|  
|La instrucción se crea con TYPE_SCROLL_INSENSITIVE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] crea un cursor de instantánea estático. Se desconecta de las filas de la tabla subyacente para ayudar a proteger el cursor de las actualizaciones de filas de otros usuarios.|Use TYPE_SCROLL_SENSITIVE, TYPE_SS_SCROLL_KEYSET, TYPE_SS_SCROLL_DYNAMIC o TYPE_FORWARD_ONLY con CONCUR_UPDATABLE para evitar crear un cursor estático.|  
|El diseño de la tabla imposibilita el uso de un cursor KEYSET o DYNAMIC|La tabla subyacente no tiene claves únicas para habilitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para identificar de forma única una fila.|Agregue claves únicas a la tabla para permitir la identificación exclusiva de cada fila.|  
  
## <a name="see-also"></a>Vea también  
 [Administrar conjuntos de resultados con el controlador JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
