---
title: Establecer parámetros en un informe publicado (Reporting Services en el modo integrado de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- report parameters [Reporting Services]
ms.assetid: dec5d985-a6c1-4dd8-8a66-a848e89a2e18
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: da71b511a65758483a9bf207dbe54a484f4f1b26
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105016"
---
# <a name="set-parameters-on-a-published-report-reporting-services-in-sharepoint-integrated-mode"></a>Establecer parámetros en un informe publicado (Reporting Services en el modo integrado de SharePoint)
  Un informe con parámetros es un informe que acepta valores de entrada usados para filtrar datos al ejecutar el informe. Los parámetros se definen al crear el informe. En función de cómo se defina un parámetro del informe en la definición del informe, puede aceptar un solo valor, varios valores o valores dinámicos, que cambian en respuesta a una selección previa (por ejemplo, si selecciona una categoría del producto, la siguiente selección podría ser un producto concreto de esa categoría). Un parámetro puede tener un valor predeterminado, que se puede usar para ejecutar una versión filtrada del informe de manera automática o posiblemente sustituirlo por otro valor.  
  
 Estas propiedades se pueden establecer en la definición de informe o una vez publicado el informe. Aunque puede modificar algunas propiedades de parámetros en un informe publicado para cambiar el valor y mostrar las propiedades, no puede cambiar el nombre de un parámetro o el tipo de datos. El nombre y el tipo de datos del parámetro solamente los puede cambiar el creador del informe en la definición de informe.  
  
 Para ejecutar un informe con parámetros, normalmente debe conocer qué valores escribir, aunque el informe puede incluir listas desplegables de valores válidos entre los que elegir.  
  
 Para establecer las propiedades de parámetros de un informe publicado, debe tener el permiso Editar elementos para el informe. Puede modificar algunas o todas las propiedades de parámetros de un informe que se ejecuta desde un sitio de SharePoint. No puede personalizar un informe si guarda una combinación de valores de parámetros que desee usar repetidamente. Cualquier valor predeterminado que especifique lo usarán todos los usuarios que abran el informe.  
  
 Si el informe se incrusta en un elemento web Visor de informes configurado para mostrar siempre ese informe, establezca las propiedades en el elemento web Visor de informes. Para más información, vea [Agregar el elemento web Visor de informes a una página web &#40;Reporting Services en el modo integrado de SharePoint&#41;](../report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="to-run-a-parameterized-report"></a>Para ejecutar un informe con parámetros  
  
1.  Abra la biblioteca que contiene el informe.  
  
2.  Haga clic en el nombre del informe. Debe saber de antemano qué informes tienen parámetros. No hay ningún identificador visual en el informe que indique que tiene parámetros.  
  
3.  Al abrirse el informe, especifique los parámetros que desea usar. El área de parámetros puede estar visible, contraída u oculta según el modo en que las propiedades estén establecidas en el elemento web Visor de informes.  
  
    1.  Si el área de parámetros está visible, elija un valor para cada parámetro.  
  
    2.  Si hay una tira fina de color a lo largo del informe con una flecha en el centro, el área de parámetros está contraída. Haga clic en la flecha para expandirla.  
  
    3.  Si el área de parámetros está oculta, no puede especificar ningún valor.  
  
4.  Haga clic en **Aplicar** en la parte inferior del área de parámetros para ejecutar el informe.  
  
     Es posible especificar una combinación de valores que no proporcione el resultado esperado. Puede ser necesario que el autor modifique el informe si no está obteniendo la información que necesita.  
  
5.  Haga clic en **OK**.  
  
### <a name="to-set-parameter-properties"></a>Para establecer las propiedades de parámetros  
  
1.  Abra la biblioteca o la carpeta que contiene el informe.  
  
2.  Seleccione el informe y haga clic en la flecha hacia abajo.  
  
3.  Haga clic en **Administrar parámetros**. Si el informe contiene parámetros, cada parámetro aparecerá en una lista en la página. En esta lista se muestra el nombre del parámetro, el tipo de datos, el valor de los datos que se usa de manera predeterminada y si está visible en el área de parámetros cuando se abre el informe.  
  
4.  Haga clic en un parámetro de la lista para modificar su configuración.  
  
5.  En Valor predeterminado, escriba un valor para el parámetro. El valor no se validará; por tanto, asegúrese de proporcionar un valor que funcione con el informe.  
  
    1.  Elija **Usar expresión de valor especificada en la definición de informe** si desea usar el valor predeterminado definido al crear el informe. Si la definición de informe no proporciona ningún valor predeterminado, esta opción no estará disponible.  
  
    2.  Elija **Omitir valor predeterminado del informe** si desea especificar un reemplazo para el valor predeterminado de la definición de informe. Opcionalmente, para los parámetros de informe que aceptan valores Null, puede activar la casilla **Null** para evitar el filtrado basado en el parámetro.  
  
    3.  Elija **El parámetro no tiene un valor predeterminado** si desea que cada usuario especifique un valor antes de procesar el informe. Si selecciona esta opción, debe establecer una configuración de visualización que solicite al usuario que especifique un valor.  
  
     Tenga en cuenta que si todos los valores de los parámetros tienen un valor predeterminado, el informe se ejecutará automáticamente con esos valores cuando el usuario abra el informe. No obstante, si se muestra el área de parámetros, los usuarios pueden reemplazar el valor predeterminado y volver a ejecutar el informe.  
  
6.  Establezca las opciones de visualización para determinar si el parámetro estará visible.  
  
    1.  Elija **Preguntar al usuario** para mostrar el parámetro en la página. Puede especificar el texto de la pregunta que aparece en un campo para ofrecer una breve indicación acerca del formato o el tipo de datos que el usuario debe proporcionar.  
  
    2.  Elija **Oculto** si está usando un valor predeterminado y no desea que el parámetro esté visible en el área de parámetros.  
  
    3.  Elija **Interno** si está usando un valor predeterminado y no desea que el parámetro esté visible en el área de parámetros o en las páginas de suscripción.  
  
7.  Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de permisos de sitio y lista de SharePoint para los elementos del servidor de informes](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
  
  
