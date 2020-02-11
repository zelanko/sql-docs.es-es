---
title: 'Tarea 6: importar valores del proyecto limpiar lista de proveedores | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f6b90a36238cd4a02e86d49125ee662f07d32882
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489096"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>Tarea 6: importar valores del proyecto Limpiar lista de proveedores
  En esta tarea, importará el conocimiento de calidad de datos obtenido durante el proceso de limpieza. Consulte [el tema importar valores de proyecto de limpieza en un dominio](https://msdn.microsoft.com/library/hh479581.aspx) para obtener más detalles. También exportará la base de conocimiento en un archivo DQS antes de publicar la base de conocimiento de **proveedores** actualizada.  
  
1.  En la Página principal del **cliente DQS**, haga clic en la **flecha derecha** junto a **proveedores** en **bases de conocimiento recientes** y haga clic en **Administración de dominios**.  
  
2.  Haga clic en **correo electrónico de contacto** en la lista de dominios y cambie a la pestaña **valores del dominio** en el panel derecho.  
  
3.  Haga clic en la **flecha abajo** situada junto al icono **importar valores** de la barra de herramientas y haga clic en **importar valores de proyecto**.  
  
     ![Botón de la barra de herramientas Importar valores de proyecto](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "Botón de la barra de herramientas Importar valores de proyecto")  
  
4.  En el cuadro de diálogo **importar valores de proyecto** , seleccione el proyecto **limpiar lista de proveedores** y haga clic en **Aceptar**.  
  
5.  Observe que se importan todas las direcciones de correo electrónico junto con las dos correcciones que hizo durante la limpieza interactiva. Desplácese para ver las dos correcciones.  
  
    |Value|Corregir a|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  Repita el paso anterior de importación de valores de proyecto para el dominio **Country** y observe que se ha agregado una nueva entrada para corregir el **Estado de United State** en **Estados Unidos** (con ' es ').  
  
    |Value|Corregir a|  
    |-----------|----------------|  
    |United State|Estados Unidos|  
  
7.  Para ver los valores de dominio antiguos, desactive la casilla **Mostrar solo nuevo** .  
  
8.  Repita el paso anterior de importación de valores de proyecto para el dominio de **nombre de proveedor** . De forma predeterminada, después de la importación, solo verá los nuevos valores. Para ver todos los valores, desactive la casilla **Mostrar solo nuevo** . Ha enriquecido la base de conocimiento **proveedores** con lo que ha aprendido en la actividad de limpieza. Cuanto más sólida sea la base de conocimiento, mejores resultados obtendrá la limpieza.  
  
    > [!NOTE]  
    >  No es posible importar valores de un dominio compuesto.  
  
9. En la barra de herramientas, haga clic en el icono **exportar base de conocimiento** y, a continuación, en **exportar base de conocimiento**.  
  
     ![Exportar menú de base de conocimiento](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "Exportar menú de base de conocimiento")  
  
10. Vaya a la carpeta tutorial, escriba **Suppliers. DQS** como **nombre de archivo**y haga clic en **Guardar**. Puede usar este archivo de DQS para crear una nueva base de conocimiento a partir de él.  
  
11. Haga clic en **Aceptar** para cerrar el cuadro de mensaje **exportar base de conocimiento-proveedores** .  
  
12. Haga clic en **Finalizar** para finalizar la actividad.  
  
13. Haga clic en **Publicar**.  
  
14. Haga clic en **Aceptar** en el cuadro de mensaje.  
  
## <a name="next-step"></a>siguiente paso  
 [Lección 3: buscar datos coincidentes para quitar duplicados de lista de proveedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
