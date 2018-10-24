---
title: Registro de cambios de SQL Server Reporting Services (SSRS) 2017 y versiones posteriores | Microsoft Docs
ms.date: 08/31/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: casualoak
ms.author: edugonz
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 2fa40e17381622862ea2a5b5e6fac594f6a42f6a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728806"
---
# <a name="change-log-for-sql-server-reporting-services-ssrs-2017-and-later"></a>Registro de cambios de SQL Server Reporting Services (SSRS) 2017 y versiones posteriores

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

En este artículo se describen los cambios en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

### <a name="version-140600906-released-september-12-2018"></a>Versión 14.0.600.906, fecha de publicación: 12 de septiembre de 2018

Este error se ha solucionado:

- La autenticación personalizada no devuelve información de cookies correcta

### <a name="version-140600892-released-august-31-2018"></a>Versión 14.0.600.892, publicada el 31 de agosto de 2018

Se han corregido estos errores:

- El cuadro de texto dentro del rectángulo hace que el rectángulo no crezca verticalmente si rc:Toolbar=False y tiene texto largo 
- El tamaño del texto no se escala si pageHeight es inferior a 0,5 pulg. 
- Interbloqueo en la base de datos de catálogos de SSRS al usarse con CRM 
- Encabezados de columna alineados de manera vertical mostrados de forma incorrecta al desplazarse hasta el informe 
- Los usuarios agregados al rol de informes SCOM tendrán bloqueado el acceso al portal web de SSRS 
- El carácter tailandés no se exporta correctamente en PDF 
- Cambio de comportamiento del rol Explorador 
- rc:Toolbar=false no funciona en Express Edition 
- Barra de desplazamiento vertical que falta en el área de mensajes del parámetro 
- Tiempo de ejecución de informes móviles actualizado 

### <a name="version-140600744-released-april-25-2018"></a>Versión 14.0.600.744, publicada el 25 de abril de 2018 

Se han corregido estos errores:

- La página Suscripción controlada por datos no muestra la opción de entrega una vez creada.
- La actualización de SSRS 2012 a SSRS 2017 tiene como resultado que RSManagement lanza una excepción cada pocos segundos.
- No se pueden modificar los valores predeterminados para parámetros de varios valores en IE11.
- Los horarios están vacíos cada vez que se ejecuta una programación compartida.

### <a name="version-140600689-released-february-28-2018"></a>Versión 14.0.600.689, publicada el 28 de febrero de 2018

Se han corregido estos errores:

- La visibilidad del parámetro de informe de un informe vinculado se revierte después de editar sus propiedades
- El parámetro de la dirección URL rc:Toolbar=false no funciona en Express Edition
- Las expresiones en TextBox con la propiedad CanGrow establecida en false hace que no se muestren los valores
- Se agregó el vínculo "Más información" para la clave de producto en la configuración
- El portal web con autenticación de formularios personalizados omite el deslizamiento de la cookie de expiración
- Exportar a Word crea un alto de fila desigual si el contenido de la fila está vacío

### <a name="version-140600594-released-january-9-2018"></a>Versión 14.0.600.594, publicada el 9 de enero de 2018

Actualizaciones de seguridad

### <a name="version-140600490-released-november-1-2017"></a>Versión 14.0.600.490, fecha de publicación: 1 de noviembre de 2017

Este error se ha solucionado:

- Problemas resueltos con la actualización de SKU

### <a name="version-140600451-released-september-30-2017"></a>Versión 14.0.600.451, fecha de publicación: 30 de septiembre de 2017 

Versión inicial

## <a name="next-steps"></a>Pasos siguientes

[Novedades de Reporting Services (SSRS)](what-s-new-in-sql-server-reporting-services-ssrs.md)   

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
