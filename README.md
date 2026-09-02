# Ex.No: 05  Implementation of Steering behaviour-Pursue and Evade in Unity
### DATE: 31/08/2026                                                           
### REGISTER NUMBER : 2305003006
### AIM: 
To write a program to simulate the process of Pursue and Evade behavior in Unity using NavigationMeshAgent. 
### Algorithm:

1. Create a New Unity Project by Open the  Unity Hub and create a new 3D Project.
2. Name the project "SteeringBehaviors" and select a location. Click Create.
3.Open Unity Scene (default is SampleScene).
  In the Hierarchy, create a Plane:
  Right-click → 3D Object → Plane (this will be the ground).
  Set its Scale to (10, 1, 10) for a larger surface.
  Create three Capsule for the Player, Pursuer, and Evader:
  Rename them to "Player", "Pursuer", and "Evader".
  Set their Y Position to 0.5 (so they sit on the ground).
  Change their Material for better distinction (optional).
3. Add NavMesh and Bake
   Window → AI → Navigation (opens the Navigation tab).
   Select the Plane, go to the Navigation tab, and mark it as Navigation Static.
   Go to the Bake tab and click Bake.
   or
   Add navMeshSurface to plane and bake 
4. Add NavMeshAgent Component
    Select Pursuer, and Evader.
    Click Add Component → Search for NavMeshAgent and add it.
    Adjust NavMeshAgent Settings:
    Player: Set Speed = 5.
    Pursuer: Set Speed = 4.
    Evader: Set Speed = 6.

5. Write a script for  Player_movement behavior and save it
#### PlayerMovement
```c#

using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    Rigidbody rb;
    [SerializeField] float walkSpeed = 10f;
    float hInput;
    float vInput;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }
    void Update()
    {
        hInput = Input.GetAxis("Horizontal");
        vInput = Input.GetAxis("Vertical");
        Vector3 direction = new Vector3(hInput,rb.velocity.y,vInput);
        rb.velocity = direction.normalized * walkSpeed;

    }

}

```
#### Evader script
```c#

using UnityEngine;
using UnityEngine.AI;

public class Evader : MonoBehaviour
{
   // Start is called before the first frame update
    public NavMeshAgent agent;
    public Transform target;
    public float evadeSpeed;
    void Start()
    {
        agent= GetComponent<NavMeshAgent>();
    }

    void evade()
    {
        Vector3 dir = transform.position - target.position;
        Vector3 evadePosition = transform.position + dir.normalized * evadeSpeed;
        agent.SetDestination(evadePosition);

    }
    // Update is called once per frame
    void Update()
    {
        evade();          
     }
}

```
#### Pursuer script
```c#
public class Pursuer: MonoBehaviour
{
    // Start is called before the first frame update
    NavMeshAgent agent;
    public Transform target;
    public float speed;
    void Start()
    {
        agent=this.GetComponent<NavMeshAgent>();
    }
       // Update is called once per frame
    void pursue()
    {
       Vector3 targetvelocity=target.position-transform.position;
       Vector3 futurepos = transform.position + targetvelocity.normalized*speed;
       agent.SetDestination(target.position);
    } 
    // Update is called once per frame
    void Update()
    {
        pursue();          
     }
}
```
7. Attach the Script to each player,pursuer and Evader.
   Drag & Drop the Target from the Hierarchy into the "Target" field in the script component ( For pursuer and Evader).
12. Run the game 
13. Stop the program
    

### Output:

#### Player
<img width="1128" height="513" alt="image" src="https://github.com/user-attachments/assets/e012aeb9-6f50-4fea-94d4-06fbd53d040a" />

#### Evader
<img width="1126" height="511" alt="image" src="https://github.com/user-attachments/assets/540be547-b530-4ca6-90a0-15e1473280ad" />

#### Pursuer
<img width="1128" height="510" alt="image" src="https://github.com/user-attachments/assets/915ea6c6-baef-489e-9382-9ec80cc0245b" />







### Result:
Thus the simple pursue and evade behavior was implemented successfully.
