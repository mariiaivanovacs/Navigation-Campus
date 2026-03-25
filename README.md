# APU Campus Virtual Tour

A comprehensive 360-degree virtual tour application for the Asia Pacific University (APU) campus, built with HTML5, JavaScript, and the Pannellum panoramic viewer library.

## Video Preview

[![Demo video](https://github.com/user-attachments/assets/af05bbb2-5b15-425a-b666-52087c2cb5ce)](https://youtu.be/2ahyZ1LY9Tk?si=5jf8SCw8n_hjZX0r)

---

## Features

### Core Functionality
- **360-degree panoramic views** of campus locations across multiple levels
- **Interactive navigation** between different campus areas and buildings
- **Smart pathfinding** with automatic route calculation between locations
- **Dual navigation modes**: Explore freely or follow guided routes to destinations
- **Multi-level support** with Level 3 and Level 4 campus areas
- **Responsive hotspot system** with visual indicators for navigation and points of interest

### Campus Coverage
- **Block A**: Reception area and administrative spaces
- **Block B**: Student services and academic facilities  
- **Block D**: Bursary, canteen, and atrium areas
- **Block E**: Additional academic spaces and tech labs
- **Library**: Dedicated library space with study areas
- **Recreational Areas**: Gym, accommodations, and Bila Bila Mart
- **Administrative Areas**: Admin office, clinic, and visa center

## Technical Stack

### Dependencies
- **Pannellum 2.5.6**: 360-degree panoramic viewer
- **Bootstrap Icons 1.11.0**: Icon library for UI elements
- **Font Awesome 6.5.0**: Additional icons and visual elements

### Browser Support
- Modern browsers with HTML5 and WebGL support
- Mobile responsive design for touch devices

## Installation & Setup

1. **Clone or download** the project files
2. **Ensure all dependencies** are properly linked (CDN links included)
3. **Add panoramic images** to the `images_dev/` directory:
   - `L3I1.JPEG` through `L3I6.JPEG` for Level 3 locations
   - `L4BA.JPEG`, `L4BBB.JPEG`, `L4BD.JPEG`, etc. for Level 4 locations
4. **Include the CSS file** (`styles.css`) with your custom styling
5. **Host on a web server** (required for proper file loading) - run a command: python3 -m http.server

## Usage

### URL Parameters
The application accepts several URL parameters for customization:

```
?start=[location]&destination=[location]&mode=[explore|navigation]
```

#### Parameters:
- **`start`**: Starting location ID (e.g., `locationALevel3`)
- **`destination`**: Target destination ID (optional)
- **`mode`**: Navigation mode (`explore` for free navigation, omit for guided routes)

#### Example URLs:
```
# Start at Block A Level 3, navigate to Library
?start=locationALevel3&destination=locationLibrary4

# Start at Reception, explore freely
?start=locationReception3&mode=explore

# Default starting location with guided tour to gym
?destination=locationGym3
```

### Navigation Modes

#### Guided Navigation Mode
- Automatically calculates optimal routes between locations
- Highlights navigation hotspots along the path
- Updates camera angles to guide users toward their destination
- Provides success notifications upon arrival

#### Explore Mode
- Free navigation between any connected locations
- All hotspots remain interactive
- No specific destination guidance

## File Structure

```
├── index.html              # Main application file
├── styles.css              # Custom styling (external)
├── images_dev/            # Panoramic images directory
│   ├── L3I1.JPEG         # Level 3 location images
│   ├── L3I2.JPEG
│   ├── ...
│   ├── L4BA.JPEG         # Level 4 location images
│   ├── L4BBB.JPEG
│   └── ...
└── navigation_menu_page.html  # Navigation menu (referenced)
```

## Locations & IDs

### Level 3 Locations
| Location ID | Display Name | Description |
|-------------|--------------|-------------|
| `locationALevel3` | Block A Level 3 | Main entrance area with reception |
| `locationBLevel3` | Block B Level 3 | Student services and academic spaces |
| `locationDLevel3` | Block D Level 3 | Bursary, canteen, and atrium |
| `locationELevel3` | Block E Level 3 | Additional academic facilities |
| `locationGymBilaMart3` | Recreational Area | Gym, accommodations, and mart |

### Level 4 Locations
| Location ID | Display Name | Description |
|-------------|--------------|-------------|
| `locationALevel4` | Block A Level 4 | Upper level of Block A |
| `locationBLevel4` | Block B Level 4 | Upper level of Block B |
| `locationDLevel4` | Block D Level 4 | Upper level of Block D |
| `locationELevel4` | Block E Level 4 | Upper level with tech labs |
| `locationLibrary4` | Library | Main library facility |
| `locationAdminClinic4` | Admin & Clinic | Administrative and health services |

### Specific Facilities
| Location ID | Display Name | Notes |
|-------------|--------------|-------|
| `locationReception3` | Reception | Maps to Block A Level 3 |
| `locationStudentServices3` | Student Services | Maps to Block B Level 3 |
| `locationCanteen3` | Canteen | Maps to Block D Level 3 |
| `locationGym3` | Gym | Maps to Recreational Area |
| `locationAdmin4` | Admin Office | Maps to Admin & Clinic |
| `locationClinic4` | Clinic | Maps to Admin & Clinic |

## Customization

### Adding New Locations

1. **Add panoramic image** to `images_dev/` directory
2. **Create scene configuration** in either `scenesLevel3` or `scenesLevel4`
3. **Update location mappings** in `locationMap` object
4. **Configure transitions** in `sceneTransitions` object
5. **Set initial camera angles** in `initialPitchYaw` object

### Hotspot Types
- **`scene`**: Navigation hotspots that link to other locations
- **`info`**: Information hotspots that display details about facilities

### CSS Classes for Hotspots
- `hotspot-navigation`: General navigation points
- `hotspot-building`: Building identifiers
- `hotspot-library`: Library-specific styling
- `hotspot-stairs`: Stair navigation points
- `hotspot-elevator`: Elevator indicators
- `hotspot-pulse`: Animated pulsing effect

## Algorithm Details

### Pathfinding System
The application uses a graph-based pathfinding algorithm:

1. **Graph Construction**: Builds a navigation graph from hotspot connections
2. **Shortest Path**: Uses breadth-first search for optimal route calculation
3. **Multi-level Routing**: Handles transitions between Level 3 and Level 4
4. **Dynamic Hotspot Updates**: Adjusts navigation indicators based on calculated path

### Route Optimization
- Automatic detection of level changes
- Stair and elevator navigation integration
- Context-aware camera positioning for optimal user guidance

## Browser Compatibility

### Minimum Requirements
- WebGL support for 3D rendering
- Modern JavaScript ES6+ support
- Touch events for mobile navigation

### Tested Browsers
- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

## Performance Considerations

- **Image Optimization**: Use compressed JPEG images for faster loading
- **Progressive Loading**: Images load as needed during navigation
- **Memory Management**: Automatic cleanup of unused panoramic data
- **Mobile Optimization**: Touch-friendly hotspot sizing and navigation

## Troubleshooting

### Common Issues

**Images not loading:**
- Verify image paths in `images_dev/` directory
- Ensure web server is running (required for local file access)
- Check browser console for 404 errors

**Navigation not working:**
- Verify hotspot `sceneId` values match location IDs
- Check `sceneTransitions` configuration for missing connections
- Ensure all referenced locations exist in scene configurations

**Camera positioning issues:**
- Review `initialPitchYaw` settings for accurate starting angles
- Verify `targetYaw` and `targetPitch` values in hotspot configurations

## Contributing

To extend or modify the virtual tour:

1. Follow the existing naming conventions for location IDs
2. Maintain consistent hotspot styling and interaction patterns
3. Test navigation paths thoroughly across all levels
4. Ensure mobile responsiveness for new features
5. Document any new location mappings or transition configurations

## License

This project is designed for educational and institutional use at Asia Pacific University.

## Support

For technical issues or feature requests, refer to the Pannellum documentation or contact the development team.
