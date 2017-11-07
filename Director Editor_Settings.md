









# Director Editor : Settings 

Director is METoolKit-based application so if you've tried METoolKit before, you may find similarities in the Project and Build settings of this project. 

Before proceeding, make sure you have the following: 

```
Unity 5.5 or later
Visual Studio 2017
Director Package with METoolkit
```

### Create a scene

1. In the **Project** panel, search for **MEHoloEntrance** prefab and drag it in the **Heirarchy**. 

2. Select MEHoloEntrance and go to the **Inspector** panel.  Add **App ID** and click on **Create All MEHolo Module** to create **MEHolo** game object that contains all Mesh Expert modules. 

3. Search for **DirectoryManager** prefab and drag it in the Heirarchy. 

4. Create an empty game object and name it **Main App**. 

5. Select MainApp object and in the Inspector click on **Add Component** -> **New Script** and name it **MainAppScript**.

6. Open your **MainAppScript** and paste the code below.

   ```c#

   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;
   using Newtonsoft.Json;
   using DataMesh.AR;
   using DataMesh.AR.Director;
   using DataMesh.AR.Interactive;

   public class MainAppScript : MonoBehaviour
   {
       private DirectorManager directorManager;
       private MultiInputManager inputManager;

       // Use this for initialization
       void Start()
       {
           StartCoroutine(WaitForInit());
       }

       private IEnumerator WaitForInit()
       {
           MEHoloEntrance entrance = MEHoloEntrance.Instance;
           while (!entrance.HasInit)
           {
               yield return null;
           }
           directorManager = DirectorManager.Instance;
           directorManager.Init();
           directorManager.TurnOn();
       }
   }
   ```

7. Save the scene to make the changes permanent. 

### Project and Build Settings

1. ​