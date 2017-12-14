---
title: "Realizando operación (Asistente para importación y exportación de SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.impexpwizard.performingoperation.f1
ms.assetid: 83259509-71d6-4a64-a7f2-4e9603b30bd4
caps.latest.revision: "42"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d31607e0a2880d0a984efe20e4b11c9195cb789
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="performing-operation-sql-server-import-and-export-wizard"></a>Operación en curso (Asistente para importación y exportación de SQL Server)
Después de revisar las opciones que ha elegido en el asistente y de hacer clic en **Finalizar** en la página **Completar el asistente** , en el Asistente para importar y exportar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se mostrará **Realizando operación**. En esta página, verá el progreso y el resultado de la operación que ha configurado en las páginas anteriores. No hace falta que realice ninguna acción en esta página.

## <a name="screen-shot---operation-in-progress"></a>Captura de pantalla: operación en curso 
 En la captura de pantalla siguiente se muestra la página **Realizando operación** del asistente mientras la operación aún está en curso.  
  
 ![Página Realizando operación del Asistente para importación y exportación](../../integration-services/import-export-data/media/performing-operation1.png "Performing operation page of the Import and Export Wizard")  

## <a name="screen-shot---operation-completed"></a>Captura de pantalla: operación completada 
 En la captura de pantalla siguiente se muestra la página **Realizando operación** del asistente después de completarse la operación. Haga clic en un elemento de la columna **Mensajes** para obtener más información sobre el paso correspondiente.  
  
 ![Página Realizando operación del Asistente para importación y exportación](../../integration-services/import-export-data/media/performing-operation2.png "Performing operation page of the Import and Export Wizard")  
  
## <a name="watch-the-progress-of-the-operation"></a>Observar el progreso de la operación
 **Acción**  
 Muestra cada paso de la operación.  
  
 **Estado**  
 Indica si el paso se completó correctamente o no.  
  
 **Mensaje**  
 Muestra mensajes de error y de información sobre el paso. Haga clic en un elemento de esta columna para obtener más información sobre el paso correspondiente.

## <a name="interrupt-the-operation-or-save-the-results"></a>Interrumpir la operación o guardar los resultados
 **Detener**  
 Si es necesario, puede interrumpir la operación si hace clic en el botón **Detener** .  
  
 **Informe**  
 Permite ver un informe de los resultados, guardarlo en un archivo, copiarlo al portapapeles o enviarlo por correo electrónico.  
  
## <a name="whats-next"></a>¿Qué sigue?  
 Cuando la operación que ha configurado se ejecute y se complete correctamente, habrá terminado de ejecutar el Asistente para importar y exportar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
-   Si ha ejecutado la operación inmediatamente, puede abrir el destino que ha seleccionado para revisar los datos que haya copiado el asistente.  
-   Si ha guardado el paquete SSIS creado por la asistente, puede abrirlo en SQL Server Data Tools para personalizarlo y volverlo a usar. Para obtener información sobre cómo personalizar el paquete guardado y volverlo ejecutar posteriormente, vea [Guardar un paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).

## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


