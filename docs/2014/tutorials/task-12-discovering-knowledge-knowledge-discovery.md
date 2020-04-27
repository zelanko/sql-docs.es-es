---
title: 'Tarea 12: detectar conocimiento (detección de conocimiento) | Microsoft Docs'
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484681"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>Tarea 12: Detección de conocimiento
  En esta tarea, realizará la actividad **detección de conocimiento** en los dominios ID. de **proveedor** y nombre de **proveedor** . En este escenario, el proceso de detección de conocimiento importa principalmente valores de estos dos dominios.  
  
 En este tutorial, empezó a crear la base de conocimiento desde el principio. También puede empezar a crear una base de conocimiento realizando una actividad de detección de conocimiento. Al hacer clic en **crear una base de conocimiento** en la Página principal, el cliente DQS le lleva a una página con la actividad **Administración de dominios** seleccionada para la actividad. Puede cambiar la **actividad** a **detección de conocimiento** y, a continuación, en la página siguiente, puede crear dominios como parte del proceso de detección de conocimiento. Vea [realizar la detección de conocimiento](https://msdn.microsoft.com/library/hh510398.aspx) para obtener más detalles.  
  
1.  En la Página principal del cliente DQS, en la sección **base de conocimiento reciente** , haga clic en la **flecha derecha** situada junto a la base de conocimiento **proveedores** y haga clic en **detección de conocimiento**. También puede hacer clic en **abrir base de conocimiento**, seleccionar **proveedores** en la **lista de bases de conocimiento**, seleccionar **detección de conocimiento** como **actividad** y hacer clic en **siguiente**.  
  
     ![Menú Detección de conocimiento en la página principal](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "Menú Detección de conocimiento en la página principal")  
  
2.  Seleccione el **archivo de Excel** para el origen de **datos**.  
  
3.  Haga clic en **examinar**, desplácese y seleccione **Suppliers. xls**y haga clic en **abrir**.  
  
4.  Seleccione **proveedores para la detección** de la **hoja de cálculo**.  
  
5.  En la **sección asignaciones** , asigne la **columna SupplierID** del archivo de **Excel** a la columna ID. de **proveedor** y nombre de **proveedor** al dominio nombre de **proveedor** mediante **listas**desplegables. El archivo de Excel contiene datos de ejemplo para los dominios ID. de **proveedor** y **nombre de proveedor** . En el proceso de detección, puede seleccionar los dominios para los que desea detectar valores. Puede crear dominios en esta página y asignar las columnas de origen a esos dominios. No es infrecuente crear dominios durante la actividad de detección de conocimiento en lugar de crear dominios durante la actividad de administración de dominios.  
  
     ![Asignar página de proceso de detección](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "Asignar página de proceso de detección")  
  
6.  Haga clic en **siguiente** para cambiar a la página **detectar** .  
  
7.  En la página **detectar** , haga clic en **iniciar** para iniciar el proceso de detección. La detección se realiza en las columnas **IdProveedor** y **nombre del proveedor** en el archivo **Suppliers. xls** . Los dominios ID. de **proveedor** y **nombre de proveedor** se deben rellenar con el conocimiento extraído de la detección.  
  
     ![Descubrir página de proceso de detección](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "Descubrir página de proceso de detección")  
  
8.  Una vez completado el análisis, revise las **estadísticas de origen** en la **pestaña generador de perfiles** en la parte inferior de la página. Observe que se han detectado 10 registros nuevos con un total de 20 valores (valores de**IdProveedor** y **nombre de proveedor** de la hoja de **cálculo de Excel**). También verá el número de valores que son nuevos, únicos, nuevos y únicos, y válidos. En el cuadro de lista de la derecha, puede ver más detalles sobre cada dominio implicado en el proceso de detección. Si mantiene el mouse sobre la barra de estado en la columna Integridad, puede ver si faltan valores en las columnas del origen.  
  
     ![Resultados de detección de conocimiento](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "Resultados de detección de conocimiento")  
  
9. Haga clic en **siguiente** para cambiar a la página **administrar valores del dominio** .  
  
10. En la página **administrar valores del dominio** , haga clic en dominio de **nombre de proveedor** en la lista de dominios.  
  
11. En el panel derecho, haga clic con el botón secundario en **Lazy Country STOREX** (observe "x" al final) y seleccione **Lazy Country Store**. DQS sugiere este cambio después de ejecutar el corrector ortográfico en el dominio. De forma predeterminada, el corrector ortográfico está habilitado en los dominios que crea.  
  
     ![Corregir nombre de proveedor- Lazy Country Store](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "Corregir nombre de proveedor- Lazy Country Store")  
  
12. En la lista valores de dominio, confirme que el valor **Lazy Country STOREX** esté establecido como error (marca roja **X** ) con **Lazy Country Store** como corrección y también el **almacén de país diferido** también se agrega como valor válido.  
  
     ![Valor de dominio y Corregir al valor](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "Valor de dominio y Corregir al valor")  
  
13. Haga clic en **Finalizar**  
  
14. En **SQL Server Data Quality Services** cuadro de diálogo, haga clic en **publicar**.  
  
15. Haga clic en **Aceptar** en el cuadro de mensaje de operación correcta.  
  
     Ha completado la primera lección del tutorial.  
  
## <a name="next-step"></a>siguiente paso  
 [Lección 2: Limpieza de datos de proveedor con la base de conocimiento Proveedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
