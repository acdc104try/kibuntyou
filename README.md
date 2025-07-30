{
  "name": "kibuntyou365",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "vite": "^4.5.0",
    "@vitejs/plugin-react": "^4.0.0"
  }
}# kibuntyouimport { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>気分帳365</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)import { useState } from 'react'

function App() {
  const [good, setGood] = useState(50)
  const [bad, setBad] = useState(50)
  const [note, setNote] = useState('')
  const [log, setLog] = useState([])
  const [comment, setComment] = useState('')

  const handleCheck = () => {
    const now = new Date().toLocaleString()

    const aiComment = bad > good
      ? 'なにか心に残ったことがあれば話してみませんか？🌱'
      : '今日は良い日だったようですね😊 明日もその調子で！'

    setComment(aiComment)

    setLog([
      ...log,
      { time: now, good, bad, note, comment: aiComment }
    ])
  }

  return (
    <div style={{ padding: 20, fontFamily: 'sans-serif' }}>
      <h1>気分帳365🌤️</h1>
      <p>良い気分（0〜100）</p>
      <input type="number" value={good} onChange={(e) => setGood(Number(e.target.value))} />
      <p>悪い気分（0〜100）</p>
      <input type="number" value={bad} onChange={(e) => setBad(Number(e.target.value))} />
      <p>今日のメモ</p>
      <input
        type="text"
        value={note}
        onChange={(e) => setNote(e.target.value)}
        placeholder="例：アニメ観た・美味しいもの食べた"
      />
      <br /><br />
      <button onClick={handleCheck}>AIコメントを見る</button>

      {comment && (
        <>
          <h3>AIコメント:</h3>
          <p>{comment}</p>
        </>
      )}

      <h3>ログ:</h3>
      <ul>
        {log.map((entry, idx) => (
          <li key={idx}>
            [{entry.time}] 良: {entry.good} / 悪: {entry.bad}｜「{entry.note}」→ {entry.comment}
          </li>
        ))}
      </ul>
    </div>
  )
}

export default App
