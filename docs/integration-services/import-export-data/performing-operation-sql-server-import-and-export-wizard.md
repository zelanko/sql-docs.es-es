---
description: Operación en curso (Asistente para importación y exportación de SQL Server)
title: Realizando operación (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.performingoperation.f1
ms.assetid: 83259509-71d6-4a64-a7f2-4e9603b30bd4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1ce2552519eeecb654478f522d3dd3b8880d2697
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88347281"
---
# <a name="performing-operation-sql-server-import-and-export-wizard"></a>Operación en curso (Asistente para importación y exportación de SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Después de revisar las opciones que ha elegido en el asistente y de hacer clic en **Finalizar** en la página **Completar el asistente** , en el Asistente para importar y exportar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se mostrará **Realizando operación**. En esta página, verá el progreso y el resultado de la operación que ha configurado en las páginas anteriores. No es necesario que realice ninguna acción en esta página.

## <a name="screen-shot---operation-in-progress"></a>Captura de pantalla: operación en curso 
 En la captura de pantalla siguiente se muestra la página **Realizando operación** del asistente mientras la operación aún está en curso.  
  
 ![Página de operación en curso del Asistente para importar y exportar](../../integration-services/import-export-data/media/performing-operation1.png "Página de operación en curso del Asistente para importar y exportar")  

## <a name="screen-shot---operation-completed"></a>Captura de pantalla: operación completada 
 En la captura de pantalla siguiente se muestra la página **Realizando operación** del asistente después de completarse la operación. Haga clic en un elemento de la columna **Mensajes** para obtener más información sobre el paso correspondiente.  
  
 ![Página de operación en curso del Asistente para importar y exportar](../../integration-services/import-export-data/media/performing-operation2.png "Página de operación en curso del Asistente para importar y exportar")  
  
## <a name="watch-the-progress-of-the-operation"></a>Observar el progreso de la operación
 **Acción**  
 Muestra cada paso de la operación.  
  
 **Estado**  
 Indica si el paso se completó correctamente o no.  
  
 **Message**  
 Muestra mensajes de error y de información sobre el paso. Haga clic en un elemento de esta columna para obtener más información sobre el paso correspondiente.

## <a name="interrupt-the-operation-or-save-the-results"></a>Interrumpir la operación o guardar los resultados
 **Detención**  
 Si es necesario, puede interrumpir la operación si hace clic en el botón **Detener** .  
  
 **Report**  
 Permite ver un informe de los resultados, guardarlo en un archivo, copiarlo al portapapeles o enviarlo por correo electrónico.  
  
## <a name="whats-next"></a>A continuación  
 Cuando la operación que ha configurado se ejecute y se complete correctamente, habrá terminado de ejecutar el Asistente para importar y exportar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
-   Si ha ejecutado la operación inmediatamente, puede abrir el destino que ha seleccionado para revisar los datos que haya copiado el asistente.  
-   Si ha guardado el paquete SSIS creado por la asistente, puede abrirlo en SQL Server Data Tools para personalizarlo y volverlo a usar. Para obtener información sobre cómo personalizar el paquete guardado y volverlo ejecutar posteriormente, vea [Guardar un paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).

## <a name="see-also"></a>Consulte también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


