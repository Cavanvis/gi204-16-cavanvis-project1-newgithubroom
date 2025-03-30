using System.Diagnostics;
using UnityEngine;

public class Player : MonoBehaviour
{
    [Header(" Settings ")]
    [SerializeField] private float screenPositonFollowthreshold;
    [SerializeField] private float moveSpeed;
    private Vector3 clickedScreenPosition;
    private bool canMove;
    void Start()
    {
        EnableMovement();

        playerTime.onTimerOver += DisableMovement;

        GameManager.onStateChange += GameStateChangedCallback;
    }

    private void OnDestroy()
    {
        playerTime.onTimerOver -= DisableMovement;
        GameManager.onStateChange -= GameStateChangedCallback;
    }
    void Update()
    {
        if(canMove)
        ManageControls();
    }

    private void ManageControls()
    {
        if(Input.GetMouseButtonDown(0))
        {
            clickedScreenPosition = Input.mousePosition;
        }
        else if(Input.GetMouseButton(0))
        {
            Vector3 difference = Input.mousePosition - clickedScreenPosition;

            Vector3 direction = difference.normalized;

            float maxScreenDistance = screenPositonFollowthreshold * Screen.height;

            if(difference.magnitude > maxScreenDistance)
            {   
                clickedScreenPosition = Input.mousePosition - direction * maxScreenDistance;
                direction = Input.mousePosition - clickedScreenPosition;
            }

            difference /= Screen.width;

            difference.z = difference.y;
            difference.y = 0;

            Vector3 playerTargerPosition = transform.position + difference * moveSpeed * Time.deltaTime;
            
            transform.position = playerTargerPosition;
        }
    }


    private void GameStateChangedCallback(GameState gameState)
    {
        switch(gameState)
        {
            case GameState.MENU:
                DisableMovement();
                break;
        }
    }

    private void EnableMovement(GameState gameState)
    {
        canMove = true;
    }

    private void EnableMovement()
    {
        canMove = true;
    }

    private void DisableMovement()
    {
        canMove = false;
    }
}
