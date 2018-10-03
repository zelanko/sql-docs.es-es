---
title: Crear un componente de tiempo de diseño de elemento de informe personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a6654b7ec23e2aae071a7e4ce6cd360b7ef10e4a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107495"
---
# <a name="creating-a-custom-report-item-design-time-component"></a>Crear un componente de tiempo de diseño de elemento de informe personalizado
  Un componente de tiempo de diseño de elemento de informe personalizado es un control que se puede utilizar en el entorno de Visual Studio Report Designer. El componente de tiempo de diseño de elemento de informe personalizado proporciona una superficie de diseño activada que puede aceptar las operaciones de arrastrar y colocar, la integración con el explorador de propiedades de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], y la capacidad de proporcionar los editores de propiedades personalizados.  
  
 Con un componente de tiempo de diseño de elemento de informe personalizado, el usuario puede colocar un elemento de informe personalizado en un informe en el entorno de diseño, establecer las propiedades de datos personalizadas en el elemento de informe personalizado y, a continuación, guardar el elemento de informe personalizado como parte del proyecto de informe.  
  
 Las propiedades que se establecen utilizando el componente de tiempo de diseño en el entorno de desarrollo se serializan y deserializan por el entorno de diseño del host y, a continuación, se guardan como elementos en el archivo de lenguaje RDL (Report Definition Language). Cuando el procesador de informes ejecuta el informe, pasa las propiedades que están establecidas utilizando el componente de tiempo de diseño a un componente de tiempo de ejecución del elemento de informe personalizado, que representa el elemento de informe personalizado y lo devuelve al procesador de informes.  
  
> [!NOTE]  
>  El componente de tiempo de diseño de elemento de informe personalizado se implementa como un componente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. En este documento se describirán los detalles de la implementación específicos al componente de tiempo de diseño del elemento de informe personalizado. Para más información sobre cómo desarrollar componentes mediante [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], vea [Componentes en Visual Studio](http://go.microsoft.com/fwlink/?LinkId=116576) en MSDN Library.  
  
 Para obtener un ejemplo de un elemento de informe personalizado totalmente implementado, vea [Ejemplos del producto SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="implementing-a-design-time-component"></a>Implementar un componente de tiempo de diseño  
 La clase principal de un componente de tiempo de diseño de elemento de informe personalizado está heredada de la clase `Microsoft.ReportDesigner.CustomReportItemDesigner`. Además de los atributos estándar utilizados para un control [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], la clase de componente debería definir un atributo `CustomReportItem`. Este atributo debe corresponder al nombre del elemento de informe personalizado como se define en el archivo reportserver.config. Para obtener una lista de atributos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], vea Atributos en la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 El ejemplo de código siguiente muestra atributos que se aplican a un control de tiempo de diseño del elemento de informe personalizado:  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>Inicializar el componente  
 Las propiedades especificadas por el usuario para un elemento de informe personalizado se pasan utilizando una clase <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>. La implementación de la clase `CustomReportItemDesigner` debería invalidar el método `InitializeNewComponent` para crear una nueva instancia de la clase <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> del componente y establecerla en los valores predeterminados.  
  
 El ejemplo de código siguiente muestra un ejemplo de un una clase de componente de tiempo de tiempo de diseño de elemento de informe personalizado que invalida el método `CustomReportItemDesigner.InitializeNewComponent` para inicializar la clase <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> del componente:  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>Modificar propiedades de componentes  
 Puede modificar las propiedades `CustomData` en el entorno de diseño de varias maneras. Puede modificar cualquier propiedad que expuesta por el componente de tiempo de diseño que esté marcada con el atributo <xref:System.ComponentModel.BrowsableAttribute> utilizando el explorador de propiedades de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Además, puede modificar las propiedades si arrastra los elementos a la superficie de diseño del elemento de informe personalizado o si hace clic con el botón derecho en el control en el entorno de diseño y selecciona **Propiedades** en el menú contextual para mostrar una ventana de propiedades personalizada.  
  
 El ejemplo de código siguiente muestra una propiedad `Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData` que tiene el atributo <xref:System.ComponentModel.BrowsableAttribute> aplicado:  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 Puede proporcionar un cuadro de diálogo de editor de propiedades personalizado al componente de tiempo de diseño. La implementación personalizada del editor de propiedades debería heredar de la clase <xref:System.ComponentModel.ComponentEditor> y debería crear una instancia de un cuadro de diálogo que se puede utilizar para la edición de propiedad.  
  
 En el ejemplo siguiente se muestra una implementación de una clase que hereda de <xref:System.ComponentModel.ComponentEditor> y muestra un cuadro de diálogo de editor de propiedades personalizado:  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 El cuadro de diálogo de editor de propiedades personalizado puede invocar al editor de expresiones del diseñador de informes. En el ejemplo siguiente, el editor de expresiones se invoca cuando el usuario selecciona el primer elemento del cuadro combinado:  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>Utilizar los verbos de diseñador  
 Un verbo de diseñador es un comando de menú vinculado a un controlador de eventos. Puede agregar verbos de diseñador que aparecerán en el menú contextual de un componente cuando el control de tiempo de ejecución del elemento de informe personalizado se utiliza en el entorno de diseño. Puede devolver la lista de verbos de diseñador disponibles desde el componente de tiempo de ejecución utilizando la propiedad `Verbs`.  
  
 El ejemplo de código siguiente muestra un verbo de diseñador y un controlador de eventos agregados a <xref:System.ComponentModel.Design.DesignerVerbCollection>, así como el código de controlador de eventos:  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>Utilizar las opciones gráficas  
 Las clases de elemento de informe personalizado también pueden implementar una clase `Microsoft.ReportDesigner.Design.Adornment`. Una opción gráfica permite al control de elemento de informe personalizado proporcionar las áreas fuera del rectángulo principal de la superficie de diseño. Estas áreas pueden administrar los eventos de interfaz de usuario, como los clics del mouse y las operaciones de arrastrar y colocar. El `Adornment` clase que se define en el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] `Microsoft.ReportDesigner` espacio de nombres es una implementación paso a través de la <xref:System.Windows.Forms.Design.Behavior.Adorner> clase se encuentra en Windows Forms. Para obtener documentación completa sobre la `Adorner` de clases, vea [información general sobre el servicio de comportamiento](http://go.microsoft.com/fwlink/?LinkId=116673) en MSDN library. Código de ejemplo que implementa un `Microsoft.ReportDesigner.Design.Adornment` de clases, vea [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
 Para obtener más información acerca de cómo programar y usar Windows Forms en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], vea estos temas en MSDN Library:  
  
-   Atributos de tiempo de diseño para componentes  
  
-   Componentes de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]  
  
-   Tutorial: Crear un control de Windows Forms que aproveche las características de tiempo de diseño de Visual Studio  
  
## <a name="see-also"></a>Vea también  
 [Arquitectura de elementos de informe personalizados](custom-report-item-architecture.md)   
 [Creación de un componente de tiempo de ejecución de elemento de informe personalizado](creating-a-custom-report-item-run-time-component.md)   
 [Bibliotecas de clases de elemento de informe personalizado](custom-report-item-class-libraries.md)   
 [Implementación de un elemento de informe personalizado](how-to-deploy-a-custom-report-item.md)  
  
  
