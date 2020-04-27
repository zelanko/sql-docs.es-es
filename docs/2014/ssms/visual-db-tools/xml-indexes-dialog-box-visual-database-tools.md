---
title: Cuadro de diálogo Índices XML (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.xmlindexes
ms.assetid: eef38310-4498-4ccc-bb77-5bbd1c7cc477
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0c946e0e195937dd2e722ac3f092a57e40427b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63228346"
---
# <a name="xml-indexes-dialog-box-visual-database-tools"></a>Índices XML (cuadro de diálogo, Visual Database Tools)
  Utilice el cuadro de diálogo **Índices XML** para crear índices para las columnas de tipo de datos XML que no pueden indizarse utilizando el cuadro de diálogo **Índice y claves** . Cada columna XML puede tener más de un índice XML, pero el primero que se cree (principal) será la base de los otros (secundarios). Si elimina el índice XML principal, también se eliminarán los índices secundarios.  
  
## <a name="options"></a>Opciones  
 **Índice XML seleccionado**  
 Enumera los índices XML existentes. Selecciónelo para mostrar sus propiedades en la cuadrícula que aparece a la derecha. Si la lista está vacía, no se ha definido ninguna para la tabla.  
  
 **Add (Agregar)**  
 Crea un nuevo índice XML.  
  
 **Eliminar**  
 Elimina el índice XML seleccionado en la lista **Índice XML seleccionado** . Si elimina el índice XML principal, se le notificará que con ello eliminará también todos los índices secundarios y que puede elegir entre continuar o cancelar la acción.  
  
 **Categoría General**  
 Expandido, muestra los campos de propiedades de **Columnas**, **Principal**y **Tipo**.  
  
 **Columnas**  
 Indica que el orden del índice es ascendente.  
  
 **Principal**  
 Indica si es el índice es principal. El primer índice XML creado en la columna será la base de los otros.  
  
 **Nombre de referencia principal**  
 Muestra el nombre del índice principal si este índice es secundario. Solo está disponible si éste índice es secundario.  
  
 **Tipo secundario**  
 Muestra el tipo de índice secundario. Solo está disponible si éste índice es secundario.  
  
 **Tipo**  
 Indica si el índice es XML.  
  
 **Categoría Identidad**  
 Expandido, muestra los campos de propiedades **Nombre** y **Descripción** .  
  
 **Nombre**  
 Muestra el nombre del índice XML. Cuando se crea un nuevo índice o una nueva clave, aparece un nombre predeterminado que se genera a partir de la tabla de la ventana que está activa en el Diseñador de tablas. Puede cambiar el nombre en cualquier momento.  
  
 **Descripción**  
 Describe el índice. Para escribir una descripción más detallada, haga clic en **Descripción** y después en el botón de puntos suspensivos ( **...** ) situado a la derecha del campo de propiedad. De este modo, obtendrá un área más grande en la que escribir el texto.  
  
 **Categoría Diseñador de tablas**  
 Expandido, muestra información sobre las propiedades de este índice XML.  
  
 **Especificación de relleno**  
 Expandido, muestra información sobre **Factor de relleno** y **Rellenar índice**.  
  
 **Factor de relleno**  
 Especifica qué porcentaje de la página de índice puede rellenar el sistema. Una vez completada una página, el sistema debe dividirla si se agregan nuevos datos, lo que afecta al rendimiento.  
  
-   El valor 100 significa que las páginas estarán llenas y que utilizarán el menor volumen posible de espacio de almacenamiento, pero es la opción menos eficiente. Este valor debe utilizarse únicamente cuando no se van a efectuar cambios en los datos, como por ejemplo, en una tabla de solo lectura.  
  
-   Un valor más bajo deja más espacio vacío en las páginas de datos, lo que reduce la necesidad de dividir las páginas de datos cuando los índices aumentan, pero requiere más espacio de almacenamiento. Este valor es más adecuado cuando se vayan a producir cambios en los datos de la tabla.  
  
 **Rellenar índice**  
 Se proporciona a las páginas de este índice el mismo porcentaje de espacio vacío (relleno) especificado en **Factor de relleno**.  
  
 **Está deshabilitado**  
 Especifica si este índice está deshabilitado. Los índices deshabilitados no admiten búsquedas ni se actualizan al agregar nuevos elementos a la tabla. Puede mejorar el rendimiento de las actualizaciones e inserciones masivas deshabilitando un índice.  
  
 **Bloqueos de página permitidos**  
 Especifique si se permite el bloqueo de páginas en este índice. Permitir o denegar el bloqueo de página afecta al rendimiento de la base de datos.  
  
 **Volver a calcular estadísticas**  
 Calcula las nuevas estadísticas cuando se crea el índice. Al volver a calcular las estadísticas, se ralentiza la generación de índices, pero suele mejorar el rendimiento de las consultas.  
  
 **Bloqueos de fila permitidos**  
 Especifique si se permite el bloqueo de filas en este índice. Permitir o denegar el bloqueo de fila afecta al rendimiento de la base de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Crear índices XML](../../relational-databases/xml/create-xml-indexes.md)  
  
  
