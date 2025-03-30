using UnityEngine;

public class Collectible : MonoBehaviour
{
    [Header(" settings ")]
    [SerializeField] private float size;

    private void Start()
    {
        GetComponent<Rigidbody>().sleepThreshold = 0;
    }

    public float GetSize()
    {
        return size;
    }
}
