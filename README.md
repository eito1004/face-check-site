# face-check-siteimport { useState } from 'react';

export default function Home() {
  const [image, setImage] = useState(null);
  const [result, setResult] = useState(null);

  const handleChange = (e) => {
    setImage(e.target.files[0]);
  };

  const handleUpload = async () => {
    if (!image) return;
    const formData = new FormData();
    formData.append('file', image);

    const res = await fetch('https://your-backend.onrender.com/analyze', {
      method: 'POST',
      body: formData,
    });

    const data = await res.json();
    setResult(data);
  };

  return (
    <div style={{ padding: 20 }}>
      <h1>顔診断サイト</h1>
      <input type="file" onChange={handleChange} />
      <button onClick={handleUpload}>診断する</button>
      {result && (
        <div>
          <p>診断結果: {result.face_type}</p>
        </div>
      )}
    </div>
  );
}
