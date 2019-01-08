---
title: Crear una entidad (Complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d354abb3-88fe-4b40-a374-f6256b84ffae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f7d9df5f8cd96421f97ecbdd0401fc87d800ffab
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52784517"
---
# <a name="create-an-entity-mds-add-in-for-excel"></a>Crear una entidad (Complemento MDS para Excel)
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], los administradores pueden crear nuevas entidades para almacenar datos. Cuando crea una entidad, debe cargar al menos una muestra de los datos que desea almacenar.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso a las áreas funcionales del **Explorador** y de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../administrators-master-data-services.md).  
  
-   Debe tener un modelo existente en el que crear la entidad. Para obtener más información, consulte [Crear un modelo &#40;Master Data Services&#41;](../create-a-model-master-data-services.md).  
  
-   Asegúrese de que los datos cumplen los siguientes requisitos:  
  
    -   Los datos deben tener una fila de encabezado.  
  
    -   Resulta útil tener las columnas **Nombre** y **Código** . **Código** es un identificador único para cada fila.  
  
    -   Debe tener al menos una fila de datos distinta del encabezado. Todas las columnas no necesitan valores, pero los datos deben ser representativos de los que estarán en la entidad.  
  
    -   Si tiene una columna que contiene un identificador único (conocido en MDS como **Código**), asegúrese de que los valores sean únicos. Si ninguna columna contiene identificadores, puede hacer que se generen automáticamente cuando se cree la entidad.  
  
    -   Asegúrese de que las celdas contienen fórmulas.  
  
    -   Asegúrese de que las celdas contienen valores de hora. Los valores de fecha se pueden guardar en MDS pero los valores de hora no.  
  
### <a name="to-create-an-entity-and-load-data"></a>Para crear una entidad y cargar datos  
  
1.  Abra o cree una hoja de cálculo de Excel que contenga los datos que desea cargar.  
  
2.  Seleccione las celdas que desea cargar en la entidad nueva.  
  
3.  En la pestaña **Datos maestros** , en el grupo **Generar modelo** , haga clic en **Crear entidad**.  
  
4.  Si se le solicita conectarse a un repositorio MDS, conéctese.  
  
5.  En el cuadro de diálogo **Crear entidad** , deje el intervalo predeterminado o cámbielo para aplicarlo a los datos que desea cargar.  
  
6.  No desactive la casilla **Mis tablas tienen encabezados** .  
  
7.  En la lista **Modelo** , seleccione un modelo.  
  
8.  En la lista **Versión** , seleccione una versión.  
  
9. En el cuadro **Nuevo nombre de entidad** , escriba un nombre para la entidad.  
  
10. En la lista **Código** , seleccione la columna que contiene identificadores únicos o haga que los códigos se generen automáticamente.  
  
11. Opcional. En la lista **Nombre** , seleccione una columna que contenga los nombres de cada miembro.  
  
12. Haga clic en **Aceptar**. Cuando haya creado la entidad correctamente, aparecerá una nueva fila de encabezado, las celdas se resaltarán y el nombre de la hoja se actualizará para coincidir con el nombre de la entidad.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   Para ver los errores producidos, en el grupo **Publicar y validar** , haga clic en **Mostrar estado**. Se muestran las columnas ValidationStatus e InputStatus. Para obtener más información, consulte [Validar datos &#40;complemento MDS para Excel&#41;](validating-data-mds-add-in-for-excel.md).  
  
-   Confirme que los atributos se crearon con el tipo de datos que esperaba.  
  
## <a name="see-also"></a>Vea también  
 [Crear un atributo basado en dominio &#40;complemento MDS para Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)  
  
  
