# Grapgics-Editor-SE
Graphics Editor
import React, { useState } from 'react';
import { 
  Square,
  Circle,
  Pencil,
  Move,
  Type,
  MinusSquare,
  PlusSquare,
  Paintbrush
} from 'lucide-react';

// Custom line icon since it's not available
const LineIcon = () => (
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="20"
    height="20"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    strokeWidth="2"
    strokeLinecap="round"
    strokeLinejoin="round"
  >
    <line x1="5" y1="19" x2="19" y2="5" />
  </svg>
);

// Custom eraser icon
const EraserIcon = () => (
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="20"
    height="20"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    strokeWidth="2"
    strokeLinecap="round"
    strokeLinejoin="round"
  >
    <path d="M20 20H7L3 16C2.5 15.5 2.5 14.5 3 14L13 4C13.5 3.5 14.5 3.5 15 4L21 10C21.5 10.5 21.5 11.5 21 12L13 20" />
  </svg>
);

// Custom shapes icon
const ShapesIcon = () => (
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="20"
    height="20"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    strokeWidth="2"
    strokeLinecap="round"
    strokeLinejoin="round"
  >
    <circle cx="7" cy="7" r="4" />
    <rect x="14" y="5" width="8" height="8" />
    <polygon points="6,17 10,21 2,21" />
  </svg>
);

const MiniPaint = () => {
  const [brushSize, setBrushSize] = useState(4);
  const [selectedTool, setSelectedTool] = useState('brush');

  const tools = [
    { id: 'move', icon: <Move size={20} />, title: 'Move Tool' },
    { id: 'select', icon: <Square size={20} />, title: 'Select' },
    { id: 'brush', icon: <Pencil size={20} />, title: 'Brush' },
    { id: 'eraser', icon: <EraserIcon />, title: 'Eraser' },
    { id: 'line', icon: <LineIcon />, title: 'Line' },
    { id: 'rectangle', icon: <Square size={20} />, title: 'Rectangle' },
    { id: 'ellipse', icon: <Circle size={20} />, title: 'Ellipse' },
    { id: 'text', icon: <Type size={20} />, title: 'Text' },
    { id: 'shape', icon: <ShapesIcon />, title: 'Shape' },
  ];

  return (
    <div className="flex h-screen bg-gray-100">
      {/* Tools Sidebar */}
      <div className="w-12 bg-gray-200 border-r border-gray-300">
        {tools.map((tool) => (
          <button
            key={tool.id}
            className={`w-full p-2 hover:bg-gray-300 transition-colors ${
              selectedTool === tool.id ? 'bg-gray-300' : ''
            }`}
            onClick={() => setSelectedTool(tool.id)}
            title={tool.title}
          >
            {tool.icon}
          </button>
        ))}
      </div>

      {/* Top Toolbar */}
      <div className="flex-1 flex flex-col">
        <div className="h-12 bg-gray-200 border-b border-gray-300 flex items-center px-4 gap-4">
          <div className="flex items-center gap-2">
            <span className="text-sm text-gray-600">Size</span>
            <input
              type="number"
              value={brushSize}
              onChange={(e) => setBrushSize(Number(e.target.value))}
              className="w-16 px-2 py-1 border border-gray-300 rounded"
              min="1"
              max="100"
            />
            <button 
              className="p-1 hover:bg-gray-300 rounded"
              onClick={() => setBrushSize(prev => Math.min(prev + 1, 100))}
            >
              <PlusSquare size={20} />
            </button>
            <button 
              className="p-1 hover:bg-gray-300 rounded"
              onClick={() => setBrushSize(prev => Math.max(prev - 1, 1))}
            >
              <MinusSquare size={20} />
            </button>
          </div>

          <button className="px-4 py-1 bg-green-500 text-white rounded hover:bg-green-600 transition-colors flex items-center gap-2">
            <Paintbrush size={16} />
            Smart brush
          </button>
        </div>

        {/* Canvas Area */}
        <div className="flex-1 bg-white p-4">
          <div className="w-full h-full bg-gradient-to-b from-sky-200 to-sky-300 rounded-lg shadow-inner">
            {/* Canvas content would go here */}
          </div>
        </div>
      </div>
    </div>
  );
};

export default MiniPaint;
