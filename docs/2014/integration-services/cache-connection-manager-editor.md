---
title: Editor del Administrador de conexiones de caché | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.cacheconnection.f1
ms.assetid: 0d8f9324-0c35-4eea-b06d-da3cc2426d2c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0802ed589813a43ffac516c05a3a52de382d36c7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061077"
---
# <a name="cache-connection-manager-editor"></a>Editor del administrador de conexiones de caché
  El administrador de conexiones de caché lee un conjunto de datos de referencia a partir de la transformación de caché o de un archivo caché (.caw) y puede guardar los datos en un archivo caché. Los datos siempre se almacenan en memoria.  
  
> [!NOTE]  
>  El administrador de conexiones de caché no admite los tipos de datos de objetos binarios grandes (BLOB) DT_TEXT, DT_NTEXT y DT_IMAGE. Si el conjunto de datos de referencia contiene un tipo de datos BLOB, se producirá un error en el componente al ejecutar el paquete. Puede utilizar el **Editor del administrador de conexiones de caché** para modificar los tipos de datos de columna.  
  
 La transformación de Búsqueda realiza búsquedas en el conjunto de datos de referencia.  
  
 En el cuadro de diálogo **Editor del administrador de conexiones de caché** se incluyen estas pestañas:  
  
-   [Ficha general](#generaltab)  
  
-   [Pestaña columnas](#columnstab)  
  
 Para obtener más información acerca del administrador de conexiones de caché, vea [Cache Connection Manager](connection-manager/cache-connection-manager.md).  
  
##  <a name="generaltab"></a> Pestaña General  
 Use la pestaña **General** del cuadro de diálogo **Editor del administrador de conexiones de caché** para indicar si la memoria caché se leerá desde un archivo o se guardará en un archivo.  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de caché en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describe la conexión. Como método recomendado, describa la conexión en función de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Utilizar la caché del archivo.**  
 Indicar si se ha de utilizar un archivo caché.  
  
> [!NOTE]  
>  El nivel de protección del paquete no se aplica al archivo caché. Si el archivo caché contiene información confidencial, utilice una lista de control de acceso (ACL) para restringir el acceso a la ubicación o carpeta en la que almacena el archivo. Solo debería permitir el acceso a ciertas cuentas. Para más información, vea [Acceso a los archivos usados por los paquetes](../../2014/integration-services/access-to-files-used-by-packages.md).  
  
 Si configura el administrador de conexiones de caché para utilizar un archivo caché, el administrador de conexiones realizará una de las siguientes acciones:  
  
-   Guardar los datos en el archivo cuando se haya configurado una transformación de caché para escribir los datos procedentes de un origen de datos del flujo de datos en el administrador de conexiones de caché. Para obtener más información, vea [Cache Transform](data-flow/transformations/cache-transform.md).  
  
-   Leer los datos desde el archivo caché.  
  
 **Nombre de archivo**  
 Escriba la ruta y el nombre de archivo del archivo caché.  
  
 **Examinar**  
 Busque el archivo caché.  
  
 **Actualizar los metadatos**  
 Elimine los metadatos de columna del administrador de conexiones de caché y vuelva a llenar el administrador de conexiones de caché con los metadatos de la columna del archivo caché seleccionado.  
  
##  <a name="columnstab"></a> Pestaña Columnas  
 Utilice la pestaña **Columnas** del cuadro de diálogo **Editor del administrador de conexiones de caché** para configurar las propiedades de cada columna en la caché.  
  
### <a name="options"></a>Opciones  
 **Columna**  
 Especifique el nombre de la columna.  
  
 **Posición de índice**  
 Define qué columnas son columnas de índice especificando la posición de índice de cada columna. El índice es una colección de una o varias columnas.  
  
 Para las columnas de no índice, la posición de índice es 0.  
  
 Para las columnas de índice, la posición de índice es un número secuencial positivo. Este número indica el orden en el que la transformación Búsqueda compara las filas del conjunto de datos de referencia con las filas del origen de datos de entrada. La columna con el mayor número de valores únicos debería tener la posición de índice más pequeña.  
  
> [!NOTE]  
>  Cuando la transformación Búsqueda se configura para utilizar un administrador de conexiones de caché, a las columnas de entrada solo se les puede asignar las columnas de índice del conjunto de datos de referencia. Asimismo, todas las columnas de índice deben estar asignadas.  
  
 **Tipo**  
 Especifica el tipo de datos de la columna.  
  
 `Length`  
 Especifica el tipo de datos de la columna. Si procede en el caso del tipo de datos, puede actualizar la `Length`.  
  
 `Precision`  
 Especifica la precisión para cierto tipo de datos de columna. La precisión es el número de dígitos de un número. Si procede en el caso del tipo de datos, puede actualizar la `Precision`.  
  
 `Scale`  
 Especifica la escala para cierto tipo de datos de columna. La escala es el número de dígitos situados a la derecha de la coma decimal de un número. Si procede en el caso del tipo de datos, puede actualizar la `Scale`.  
  
 `Code Page`  
 Especifica la página de códigos para el tipo de columna. Si procede en el caso del tipo de datos, puede actualizar la `Code Page`.  
  
## <a name="see-also"></a>Vea también  
 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)  
  
  
