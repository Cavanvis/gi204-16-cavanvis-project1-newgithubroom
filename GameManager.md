using UnityEngine;
using System;
using System.Collections;

public enum GameState { MENU, GAMEPLAY, LEVELCOMPLETE, GAMEOVER, GAME }

public class GameManager : MonoBehaviour
{
    [Header(" Settings ")]
    private GameState gameState;


    [Header(" Events ")]
    public static Action<GameState> onStateChange;


    void Start()
    {
           

        gameState = GameState.MENU;
        onStateChange?.Invoke(gameState);
    }

    void Update()
    {
        
    }

    public void SetGameState()
    {
        gameState = GameState.GAME;
        onStateChange?.Invoke(gameState);
    }
}
