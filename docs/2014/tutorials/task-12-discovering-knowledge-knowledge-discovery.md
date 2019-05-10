---
title: 'Tarea 12: Detectar conocimiento (detección de conocimiento) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6dd54475ee63b2f6ef5e1b56b94c11aafd5996ff
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484681"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>Tarea 12: Detección de conocimiento
  En esta tarea, realizará la **Knowledgediscovery** actividad en **Id. de proveedor** y **Supplier Name** dominios. En este escenario, el proceso de detección de conocimiento importa principalmente valores de estos dos dominios.  
  
 En este tutorial, empezó a crear la base de conocimiento desde el principio. También puede empezar a crear una base de conocimiento realizando una actividad de detección de conocimiento. Al hacer clic en **crear una Base de conocimiento** en la página principal, el cliente DQS le lleva a una página con **Domain Management** actividad seleccionada para la actividad. Puede cambiar el **actividad** a **Knowledgediscovery** y, a continuación, en la página siguiente puede crear dominios como parte del proceso de detección de conocimiento. Consulte [Perform Knowledge Discovery](https://msdn.microsoft.com/library/hh510398.aspx) para obtener más detalles.  
  
1.  En la página principal del cliente de DQS, en el **Base de conocimiento reciente** sección, haga clic en **flecha derecha** junto a la **proveedores** knowledge base y haga clic en **conocimiento Detección**. Como alternativa, puede hacer clic en **abrir Base de conocimiento**, seleccione **proveedores** desde el **lista de bases de conocimiento**, seleccione **Knowledgediscovery**como **actividad** y haga clic en **siguiente**.  
  
     ![Menú de la detección de conocimiento en Main página](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "menú de detección de conocimiento en Main página")  
  
2.  Seleccione **el archivo de Excel** para **origen de datos**.  
  
3.  Haga clic en **examinar**, desplácese y seleccione **Suppliers.xls**y haga clic en **abierto**.  
  
4.  Seleccione **Suppliers for Discovery** para **hoja de cálculo**.  
  
5.  En el **asignaciones** sección, asigne **SupplierID** columna desde la **Excel** del archivo a la **Id. de proveedor** dominio y  **Nombre de proveedor** columna a la **Supplier Name** dominio mediante el uso de **listas desplegables**. El archivo de Excel incluye datos de ejemplo para el **Id. de proveedor** y **Supplier Name** dominios. En el proceso de detección, puede seleccionar los dominios para los que desea detectar valores. Puede crear dominios en esta página y asignar las columnas de origen a esos dominios. No es infrecuente crear dominios durante la actividad de detección de conocimiento en lugar de crear dominios durante la actividad de administración de dominios.  
  
     ![Asignar la página del proceso de detección](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "asignar la página del proceso de detección")  
  
6.  Haga clic en **siguiente** para cambiar a la **Discover** página.  
  
7.  En el **Discover** página, haga clic en **iniciar** para iniciar el proceso de detección. La detección se realiza en las columnas **SupplierID** y **Supplier Name** en el **Suppliers.xls** archivo. El **Id. de proveedor** y **Supplier Name** dominios deben rellenarse con el conocimiento extraído de la detección.  
  
     ![Descubrir página de proceso de detección](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "descubrir página de proceso de detección")  
  
8.  Una vez completado el análisis, revise el **estadísticas de origen** en el **ficha Profiler** en la parte inferior de la página. Tenga en cuenta que 10 nuevos registros con 20 valores en total (**SupplierID** y **Supplier Name** los valores de la **hoja de cálculo de Excel**) detectados. También verá el número de valores que son nuevos, únicos, nuevos y únicos, y válidos. En el cuadro de lista de la derecha, puede ver más detalles sobre cada dominio implicado en el proceso de detección. Si mantiene el mouse sobre la barra de estado en la columna Integridad, puede ver si faltan valores en las columnas del origen.  
  
     ![Resultados de la detección de conocimiento](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "resultados de la detección de conocimiento")  
  
9. Haga clic en **siguiente** para cambiar a la **administrar valores del dominio** página.  
  
10. En el **administrar valores del dominio** página, haga clic en **Supplier Name** dominio en la lista de dominios.  
  
11. En el panel derecho, haga clic en **Lazy Country Storex** (Observe la 'x' al final) y seleccione **Lazy Country Store**. DQS sugiere este cambio después de ejecutar el corrector ortográfico en el dominio. De forma predeterminada, el corrector ortográfico está habilitado en los dominios que crea.  
  
     ![Corrija el nombre de proveedor - Lazy Store del país](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "corrija el nombre de proveedor - Lazy Store del país")  
  
12. En la lista de valores de dominio, confirme que el valor **Lazy Country Storex** se establece como un error (rojo **X** marcar) con **Lazy Country Store** como la corrección y también el **Lazy Country Store** también se agrega como un valor válido.  
  
     ![Dominio de valor y corregir al valor](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "dominio valor y corregir al valor")  
  
13. Haga clic en **Finalizar**.  
  
14. En **SQL Server Data Quality Services** cuadro de diálogo, haga clic en **publicar**.  
  
15. Haga clic en **Aceptar** en el cuadro de mensaje de éxito.  
  
     Ha completado la primera lección del tutorial.  
  
## <a name="next-step"></a>Paso siguiente  
 [Lección 2: Limpieza de datos de proveedor con la Base de conocimiento proveedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
