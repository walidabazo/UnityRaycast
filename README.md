# UnityRaycast
Unity3d Raycast Camera

## Create Raycast 
    void Update()
    {
    if (Input.GetMouseButtonDown(0))
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            RaycastHit hit;
            if (Physics.Raycast(ray, out hit))
            {

                //case 1
                if (hit.collider.tag == "tag1")
                {
                }
                
                  //case 2
                if (hit.collider.tag == "tag2")
                {
                }
             }
        }    
    }
   
## To Cearte class using ITrackableEventHandler

// 1- add Reference 

    using Vuforia;

// 2-Add
  
    public class Class_name : MonoBehaviour, ITrackableEventHandler {}

// 3- Add  
  
    protected TrackableBehaviour mTrackableBehaviour;

// 4 - on Start class 
   
    void Start()
     {
         mTrackableBehaviour = GetComponent<TrackableBehaviour>();
        if (mTrackableBehaviour)
        {
            mTrackableBehaviour.RegisterTrackableEventHandler(this);
        }
        
// 5- OnTrackableStateChanged

    public void OnTrackableStateChanged(
    TrackableBehaviour.Status previousStatus,
    TrackableBehaviour.Status newStatus)
    {
        if (newStatus == TrackableBehaviour.Status.DETECTED ||
            newStatus == TrackableBehaviour.Status.TRACKED ||
            newStatus == TrackableBehaviour.Status.EXTENDED_TRACKED)
        {
   
            Debug.Log("Trackable " + mTrackableBehaviour.TrackableName + " found");

            if (mTrackableBehaviour.TrackableName == "Marker_name")
            {         
            
            }
           OnTrackingFound();
         }
       else if (previousStatus == TrackableBehaviour.Status.TRACKED &&
                 newStatus == TrackableBehaviour.Status.NOT_FOUND)
        {
            Debug.Log("Trackable " + mTrackableBehaviour.TrackableName + " lost");
            OnTrackingLost();
        }
        else
        {
            // For combo of previousStatus=UNKNOWN + newStatus=UNKNOWN|NOT_FOUND
            // Vuforia is starting, but tracking has not been lost or found yet
            // Call OnTrackingLost() to hide the augmentations
            OnTrackingLost();
        }
    }

6- // Use this for initialization


    protected virtual void OnTrackingFound()
    {
        var rendererComponents = GetComponentsInChildren<Renderer>(true);
        var colliderComponents = GetComponentsInChildren<Collider>(true);
        var canvasComponents = GetComponentsInChildren<Canvas>(true);

        // Enable rendering:
        foreach (var component in rendererComponents)
            component.enabled = true;

        // Enable colliders:
        foreach (var component in colliderComponents)
            component.enabled = true;

        // Enable canvas':
        foreach (var component in canvasComponents)
            component.enabled = true;
    }


    protected virtual void OnTrackingLost()
    {
        var rendererComponents = GetComponentsInChildren<Renderer>(true);
        var colliderComponents = GetComponentsInChildren<Collider>(true);
        var canvasComponents = GetComponentsInChildren<Canvas>(true);

        // Disable rendering:
        foreach (var component in rendererComponents)
            component.enabled = false;

        // Disable colliders:
        foreach (var component in colliderComponents)
            component.enabled = false;

        // Disable canvas':
        foreach (var component in canvasComponents)
            component.enabled = false;
    }
## AudioSource C# on unity 
   
    Gameobject.GetComponent<AudioSource>().Play();
    Gameobject.GetComponent<AudioSource>().Stop();
    Gameobject.GetComponent<AudioSource>().Pause();
    
## Video C# on unity 
// add Reference 
using UnityEngine.Video;

    Gameobject.GetComponent<VideoPlayer>().Play();
    Gameobject.GetComponent<VideoPlayer>().Stop();
    Gameobject.GetComponent<VideoPlayer>().Pause();
