using UnityEngine;

public class UIManager : MonoBehaviour
{
    [Header(" Elements ")]
    [SerializeField] private GameObject menuPanel;
    [SerializeField] private GameObject gamePanel;

    void Start()
    {
        GameManager.onStateChange += GameStateChangedCallback;
    }

    private void OnDestroy()
    {
        GameManager.onStateChange -= GameStateChangedCallback;
    }

    void Update()
    {
        
    }

    private void GameStateChangedCallback(GameState gameState)
    {
        switch(gameState)
        {

            case GameState.MENU:
                SetMenu();
                break;

            case GameState.GAME:
                SetGame();
                break;
        }
    }

    private void SetMenu()
    {
        menuPanel.SetActive(true);
        gamePanel.SetActive(false);
    }

    private void SetGame()
    {
        menuPanel.SetActive(false);
        gamePanel.SetActive(true);
    }

}
