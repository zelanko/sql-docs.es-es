---
title: 'Tarea 6: Importar valores desde el proveedor proyecto limpiar lista | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5ac003c18ae36f4cd2d58a1355df16d6d2f9b066
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359857"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>Tarea 6: importar valores del proyecto Limpiar lista de proveedores
  En esta tarea, importará el conocimiento de calidad de datos obtenido durante el proceso de limpieza. Consulte [importar valores de proyecto de limpieza en un dominio](https://msdn.microsoft.com/library/hh479581.aspx) tema para obtener más detalles. Exportar también la base de conocimiento en un archivo DQS antes de publicar la actualización **proveedores** knowledge base.  
  
1.  En la página principal de **cliente DQS**, haga clic en **flecha derecha** junto a **proveedores** en **base de conocimiento reciente** y haga clic en **Administración de dominios**.  
  
2.  Haga clic en **correo electrónico de contacto** en la lista de dominios y cambie a la **valores del dominio** en el panel derecho.  
  
3.  Haga clic en **flecha abajo** junto a la **importar valores** en la barra de herramientas y haga clic en icono **importar valores de proyecto**.  
  
     ![Botón de barra de herramientas de valores de proyecto de importación](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "importar botón de barra de herramientas de los valores de proyecto")  
  
4.  En el **importar valores de proyecto** cuadro de diálogo, seleccione el **limpiar lista de proveedores** del proyecto y haga clic en **Aceptar**.  
  
5.  Observe que se importan todas las direcciones de correo electrónico junto con las dos correcciones que hizo durante la limpieza interactiva. Desplácese para ver las dos correcciones.  
  
    |Valor|Corregir a|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  Repita el paso anterior de importar valores de proyecto para el **país** dominio y tenga en cuenta que se agrega una nueva entrada para corregir **United State** a **Estados Unidos** (con ' s').  
  
    |Valor|Corregir a|  
    |-----------|----------------|  
    |United State|United States|  
  
7.  Para ver los valores de dominio anteriores, desactive **mostrar solo nuevo** casilla de verificación.  
  
8.  Repita el paso anterior de importar valores de proyecto para el **Supplier Name** dominio. De forma predeterminada, después de la importación, solo verá los nuevos valores. Para ver todos los valores, desactive **mostrar solo nuevo** casilla de verificación. Ha enriquecido la **proveedores** base de conocimiento con lo que aprendió de la actividad de limpieza. Cuanto más sólida sea la base de conocimiento, mejores resultados obtendrá la limpieza.  
  
    > [!NOTE]  
    >  No es posible importar valores de un dominio compuesto.  
  
9. Haga clic en **Exportar Base de conocimiento** icono en la barra de herramientas y, a continuación, haga clic en **Exportar Base de conocimiento**.  
  
     ![Exportar menú de la Base de conocimiento](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "exportar menú de la Base de conocimiento")  
  
10. Vaya a la carpeta Tutorial, escriba **Suppliers.dqs** para el **nombre de archivo**y haga clic en **guardar**. Puede usar este archivo de DQS para crear una nueva base de conocimiento a partir de él.  
  
11. Haga clic en **Aceptar** para cerrar el **Exportar Base de conocimiento - proveedores** cuadro de mensaje.  
  
12. Haga clic en **finalizar** para finalizar la actividad.  
  
13. Haga clic en **Publicar**.  
  
14. Haga clic en **Aceptar** en el cuadro de mensaje.  
  
## <a name="next-step"></a>Paso siguiente  
 [Lección 3: Buscar datos coincidentes para quitar duplicados de lista de proveedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
