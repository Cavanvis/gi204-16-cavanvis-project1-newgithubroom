using System.Runtime.CompilerServices;
using Unity.Cinemachine;
using UnityEngine;

public class CameraManager : MonoBehaviour
{
    [Header(" Elements ")]
    [SerializeField] private CinemachineCamera pLayerCamera;

    [Header(" Settings ")]
    [SerializeField] private float miniDistance;
    [SerializeField] private float distanceMultiplier;

    void Start()
    {
        PlayerSize.onIncrease += PlayerSizeIncrease;
    }

    private void OnDestroy()
    {
        PlayerSize.onIncrease -= PlayerSizeIncrease;
    }

    void Update()
    {

    }

    private void PlayerSizeIncrease(float playerSize)
    {
        float distance = miniDistance + (playerSize - 1) * distanceMultiplier;

        Vector3 targetCameraPosition = new Vector3(0, distance * 1.5f, -distance);

        LeanTween.value(gameObject, GetFollowOffset(distance), targetCameraPosition, 1f)
            .setOnUpdate((Vector3 offset) => 
            {
                var followComponent = pLayerCamera.GetComponent<CinemachineFollow>();
                if (followComponent != null)
                {
                    followComponent.FollowOffset = offset;
                }
            });
        var followComponent = pLayerCamera.GetComponent<CinemachineFollow>();
        if (followComponent != null)
        {
            followComponent.FollowOffset = new Vector3(0, distance * 1.5f, -distance);
        }
        // Corrected or removed the undefined method
                LeanTween.value(gameObject, GetFollowOffset(distance), targetCameraPosition, 1f)
                    .setOnUpdate((Vector3 offset) => 
                    {
                        var followComponent = pLayerCamera.GetComponent<CinemachineFollow>();
                        if (followComponent != null)
                        {
                            followComponent.FollowOffset = offset;
                        }
                    });
        
    }
    private Vector3 GetFollowOffset(float distance)
        {
            var followComponent = pLayerCamera.GetComponent<CinemachineFollow>();
            return followComponent != null ? followComponent.FollowOffset : Vector3.zero;
        }
    
}
