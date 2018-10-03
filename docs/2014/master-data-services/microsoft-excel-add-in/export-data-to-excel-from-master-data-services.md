---
title: Cargar datos de MDS en Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 143746cb73100a28fa6ebd2fc85809bc2cfb9d41
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079965"
---
# <a name="load-data-from-mds-into-excel"></a>Cargar datos de MDS en Excel
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], debe cargar los datos del repositorio MDS para poder trabajar con él.  
  
 Si desea filtrar el conjunto de datos antes de la carga, consulte [filtrar datos antes de la carga &#40;complemento MDS para Excel&#41; ](filter-data-before-exporting-mds-add-in-for-excel.md) en su lugar.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
### <a name="to-load-data-from-mds-into-excel"></a>Para cargar datos de MDS en Excel  
  
1.  Abra Excel y, en la pestaña **Datos maestros** , conéctese a un repositorio MDS. Para obtener más información, consulte [Conectarse a un repositorio MDS &#40;complemento MDS para Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  En el panel **Explorador de datos maestros** , seleccione un modelo y una versión. La lista de entidades se rellena.  
  
    -   Si el panel **Explorador de datos maestros** no está visible, en el grupo **Conectar y cargar** , haga clic en **Mostrar explorador**.  
  
    -   Si el panel **Explorador de datos maestros** está deshabilitado, se debe a que la hoja existente ya contiene datos administrados por MDS. Para habilitar el panel, abra una nueva hoja de cálculo.  
  
3.  En el panel **Explorador de datos maestros** , en la lista de entidades, haga doble clic en la entidad que quiera cargar.  
  
    > [!NOTE]  
    >  -   Solo se carga en Excel el primer millón de miembros. Para filtrar la lista antes de la carga, en la cinta de opciones, en el grupo **Conectar y cargar** , haga clic en **Filtrar**.  
    > -   En las columnas que son listas restringidas (atributos basados en dominio), solo se cargan los 25.000 primeros valores. Puede cambiar este número en la propiedad MaximumDbaEntitySize en el archivo de excelusersettings.config ubicado en el equipo en el que está instalado Excel. Este archivo se encuentra en C:\Users\\< usuario\>\AppData\Local\Microsoft\Microsoft SQL Server\120\MasterDataServices\\.  
  
    > [!NOTE]  
    >  Al cargar datos delimitados con texto mediante el complemento para Microsoft Excel con Excel de 32 bits y los valores de las propiedades **Cell Count to Load** (Recuento de celdas que se cargarán) y **Cell Count to Publish** (Recuento de celdas que se publicarán) se establecen en un máximo de 1000, se producirá un error de memoria insuficiente. Tiene que usar Excel de 64 bits para poder usar los valores máximos en **Cell Count to Load** (Recuento de celdas que se cargarán) y **Cell Count to Publish**(Recuento de celdas que se publicarán).  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Publicar datos de Excel en MDS &#40;complemento MDS para Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Vea también  
 [Cargando datos &#40;complemento MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Cuadro de diálogo Filtrar &#40;Complemento MDS para Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [Publicar datos &#40;complemento MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
